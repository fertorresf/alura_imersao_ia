Editando... 

Desafio 1:

Meu Prompt: elabore uma query sql para oracle database, verificando em tabela de historico se possui muitas antecipações dentro de um ano

Resposta: Consultando Antecipações no Histórico do Oracle
A seguir, apresento duas opções de queries SQL para verificar a quantidade de antecipações em um histórico no Oracle, considerando um período de um ano:
Opção 1: Utilizando COUNT e GROUP BY
SELECT 
    cliente_id,
    COUNT(*) AS total_antecipacoes
FROM 
    historico_antecipacoes
WHERE 
    data_antecipacao >= ADD_MONTHS(SYSDATE, -12) -- Considera o último ano
GROUP BY 
    cliente_id
HAVING 
    COUNT(*) > X -- Substitua X pelo número mínimo de antecipações considerado "muitas"
ORDER BY 
    total_antecipacoes DESC;
Use code with caution.
SQL
Opção 2: Utilizando janela analítica com ROW_NUMBER
SELECT *
FROM (
    SELECT 
        cliente_id,
        data_antecipacao,
        ROW_NUMBER() OVER (PARTITION BY cliente_id ORDER BY data_antecipacao) AS num_antecipacoes
    FROM 
        historico_antecipacoes
    WHERE 
        data_antecipacao >= ADD_MONTHS(SYSDATE, -12) -- Considera o último ano
)
WHERE 
    num_antecipacoes > X -- Substitua X pelo número mínimo de antecipações considerado "muitas"
ORDER BY 
    cliente_id, num_antecipacoes;
Use code with caution.
SQL
Explicação das Queries:
Ambas queries consideram o período de um ano: A cláusula WHERE filtra as antecipações com data dentro do último ano, utilizando ADD_MONTHS(SYSDATE, -12).
Opção 1:
Agrupa as antecipações por cliente_id e conta o número de antecipações para cada cliente.
A cláusula HAVING filtra os resultados, mostrando apenas os clientes que tiveram mais do que X antecipações.
Opção 2:
Utiliza uma janela analítica com ROW_NUMBER() para numerar as antecipações de cada cliente, ordenadas por data.
A cláusula WHERE filtra os resultados, mostrando apenas as linhas onde o número de antecipações é maior do que X.
Adaptações:
Nome da tabela: Substitua historico_antecipacoes pelo nome da sua tabela de histórico.
Colunas:
Adapte cliente_id e data_antecipacao de acordo com os nomes das colunas na sua tabela.
Caso necessário, adicione outras colunas na consulta (ex: valor da antecipação).
Número mínimo de antecipações: Substitua X pelo valor que define o que é considerado "muitas" antecipações.
Considerações:
Estas queries assumem que a data de antecipação está armazenada em uma coluna com tipo de dado DATE.
As opções apresentadas oferecem abordagens diferentes para a mesma tarefa. A escolha entre elas dependerá das suas necessidades e preferências.

Meu Prompt: Elabore uma query SQL para database oracle, esta query está relacionada a prevenção a lavagem de dinheiro e financiamento ao terrorismo, faz-se uma verificação na tabela historico de pagamentos do cliente, verificando se possui muitas antecipações em 3 meses seguidos e/ou em um intervalo de 2 meses dentro de 1 ano, explique passo a passo detalhadamente

Resposta: Query para Detecção de Padrões Suspeitos de PLD/FT
A seguir, apresento uma query SQL para Oracle que analisa o histórico de pagamentos de um cliente, buscando padrões suspeitos relacionados a lavagem de dinheiro e financiamento ao terrorismo, considerando antecipações em períodos específicos:
WITH PagamentosAntecipados AS (
    SELECT 
        cliente_id,
        data_pagamento,
        EXTRACT(MONTH FROM data_pagamento) AS mes,
        EXTRACT(YEAR FROM data_pagamento) AS ano,
        CASE 
            WHEN data_pagamento < data_vencimento 
            THEN 1 
            ELSE 0 
        END AS is_antecipado
    FROM 
        historico_pagamentos
    WHERE 
        data_pagamento >= ADD_MONTHS(SYSDATE, -12) -- Considera o último ano
),
ContagemMensal AS (
    SELECT 
        cliente_id,
        ano,
        mes,
        SUM(is_antecipado) AS total_antecipacoes
    FROM 
        PagamentosAntecipados
    GROUP BY 
        cliente_id, ano, mes
),
MesesConsecutivos AS (
    SELECT 
        cliente_id,
        ano,
        mes,
        total_antecipacoes,
        ROW_NUMBER() OVER (PARTITION BY cliente_id, ano ORDER BY mes) AS sequencia_mes
    FROM 
        ContagemMensal
),
GruposConsecutivos AS (
    SELECT 
        cliente_id,
        ano,
        MIN(mes) AS primeiro_mes,
        MAX(mes) AS ultimo_mes,
        SUM(total_antecipacoes) AS total_antecipacoes_grupo
    FROM
        MesesConsecutivos
    GROUP BY 
        cliente_id, ano, sequencia_mes - mes
)
SELECT 
    p.cliente_id,
    p.ano,
    p.primeiro_mes,
    p.ultimo_mes,
    p.total_antecipacoes_grupo
FROM 
    GruposConsecutivos p
WHERE 
    (p.ultimo_mes - p.primeiro_mes + 1) >= 3 -- Três meses consecutivos
    OR (
        p.ultimo_mes - p.primeiro_mes = 1 
        AND p.total_antecipacoes_grupo >= 2 -- Dois meses em intervalo de um mês
    );
Use code with caution.
SQL
Explicação Passo a Passo:
PagamentosAntecipados:
Seleciona os dados relevantes do histórico de pagamentos: cliente_id, data_pagamento, mês, ano e um flag is_antecipado que indica se o pagamento foi antecipado.
Filtra os pagamentos do último ano.
ContagemMensal:
Agrupa os pagamentos por cliente, ano e mês, e calcula o total de antecipações em cada mês.
MesesConsecutivos:
Adiciona um número sequencial para cada mês dentro de cada ano para cada cliente, permitindo identificar meses consecutivos.
GruposConsecutivos:
Agrupa os meses consecutivos, identificando o primeiro e último mês do grupo e somando o total de antecipações nesse período.
Seleção Final:
Filtra os grupos de meses consecutivos que atendem aos critérios:
Três ou mais meses consecutivos com antecipações.
Dois meses dentro de um intervalo de um mês com duas ou mais antecipações.
Adaptações:
Nome da tabela: Substitua historico_pagamentos pelo nome da sua tabela de histórico.
Colunas:
Adapte cliente_id, data_pagamento e data_vencimento de acordo com os nomes das colunas na sua tabela.
Critérios de detecção: Ajuste as condições na seleção final para refletir seus critérios específicos de detecção de padrões suspeitos.
Considerações:
Essa query é um exemplo e pode precisar de ajustes dependendo do seu contexto específico e regras de negócio.
É importante combinar essa análise com outras técnicas de detecção de PLD/FT para uma abordagem mais abrangente.
Recomendações:
Considere a implementação de um sistema de pontuação de risco para avaliar a probabilidade de PLD/FT com base em diversos fatores.
Monitore as transações e padrões de comportamento dos clientes ao longo do tempo.
Implemente políticas e procedimentos de KYC (Know Your Customer) para conhecer melhor seus clientes.
Lembre-se: A prevenção à lavagem de dinheiro e financiamento ao terrorismo é uma tarefa complexa que requer uma abordagem multifacetada.
