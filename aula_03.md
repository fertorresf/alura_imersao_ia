# Aula 03: Explorando os parâmetros do Google AI Studio

# Introdução

Nesta aula, vamos ver mais sobre o Google AI Studio e explorar seus parâmetros e configurações até o suporte do modelo multimodal que o Gemini nos dá, iniciando a automação desse modelo com as APIs.

Nesta aula, você vai:
Conhecer os 3 tipos de prompts do Google AI Studio: chat prompts, freeform prompts e structured prompts;
Explorar os parâmetros do Google AI Studio;
Conhecer mais sobre os tokens e PLN;
Iniciar o contato com Python pelo Google Colab.
Link do projeto:
Acesse o Google AI Studio aqui https://aistudio.google.com/app/prompts/new_chat/?utm_source=website&utm_medium=referral&utm_campaign=Alura&utm_content=
Acesse o Google API Key aqui https://aistudio.google.com/app/apikey/?utm_source=website&utm_medium=referral&utm_campaign=Alura&utm_content=
Acesse o Google Colab aqui http://colab.research.google.com/
Acesse os prompts dessa aula aqui https://docs.google.com/document/d/1HSBfjW8nVnDp3PG9KCLspzkdxlRZDL-YnubpFI369uQ/edit?usp=sharing

> [!TIP]
> ## Desafio 1: Criar seu próprio áudio e realizar um prompt para análise pelo Google AI Studio;

> [!TIP]
> ## Desafio 2: Pesquise como colocar a imagem do Google AI Studio dentro do código de Pyhton no Google Colab;

# Links importantes para vocẽ acompanhar a aula

Guia de Mergulho da Imersão IA! https://grupoalura.notion.site/Imers-o-IA-Guia-de-Mergulho-41ae5fadd8fd47899167a115e96244d9
Acesse o Discord https://discord.gg/Dw6zBZAFU9
Acesse o Google AI Studio aqui https://aistudio.google.com/app/prompts/new_chat/?utm_source=website&utm_medium=referral&utm_campaign=Alura&utm_content=
Acesse o Google API Key aqui https://aistudio.google.com/app/apikey/?utm_source=website&utm_medium=referral&utm_campaign=Alura&utm_content=
Galeria de prompts do Google AI Studio https://ai.google.dev/examples?hl=pt-br
Vlog do Fabrício Carraro no Japão https://www.youtube.com/watch?v=dWO-9SyD7yc
Guia em PDF de Nara e Kyoto https://drive.google.com/file/d/1vByLRS3AED7NxrkgLTl2Haay53lylopr/view?usp=sharing
Live 08/05 às 18:30 | Masterclass em Python: Prepare-se para criar o seu chatbot https://youtube.com/live/j_0HRH7gZtA

# Mergulhe mais profundo

Aprofunde-se nos seguintes tópicos:
Google I/O, desenvolvimento responsável e modelos multimodais | Hipsters: Fora de Controle #05 https://www.hipsters.tech/google-i-o-desenvolvimento-responsavel-modelos-multimodais-hipsters-fora-de-controle-05/
O que é Machine Learning? https://www.alura.com.br/artigos/machine-learning?_gl=1*1di7uov*_ga*NDY2NTQxMDY5LjE3MTE0MDc0MDQ.*_ga_1EPWSW3PCS*MTcxNTM1MTAzMC4yMC4wLjE3MTUzNTEwMzAuMC4wLjA.*_fplc*NVl0RWdzOTd2RkRWTk5OJTJCTkRNN1NlYjhIOE1jRkwzUiUyRllLSE5waWlseGtuS2dQWFBFdzU1SmlXeDRTc3VlelBOWlNnN1clMkZWcm5neXNFJTJGJTJCOXUxSUpURWdrREk1aW14UmcwZ3Y0OCUyRkpmenNvdkkwZXhiJTJCRWhXY282S0lPTnclM0QlM0Q.
O que é PLN? https://www.alura.com.br/artigos/o-que-e-pln?_gl=1*1jhho6k*_ga*NDY2NTQxMDY5LjE3MTE0MDc0MDQ.*_ga_1EPWSW3PCS*MTcxNTM1MTAzMC4yMC4wLjE3MTUzNTEwMzAuMC4wLjA.*_fplc*NVl0RWdzOTd2RkRWTk5OJTJCTkRNN1NlYjhIOE1jRkwzUiUyRllLSE5waWlseGtuS2dQWFBFdzU1SmlXeDRTc3VlelBOWlNnN1clMkZWcm5neXNFJTJGJTJCOXUxSUpURWdrREk1aW14UmcwZ3Y0OCUyRkpmenNvdkkwZXhiJTJCRWhXY282S0lPTnclM0QlM0Q.
Guia de Python https://www.alura.com.br/artigos/python?_gl=1*1jhho6k*_ga*NDY2NTQxMDY5LjE3MTE0MDc0MDQ.*_ga_1EPWSW3PCS*MTcxNTM1MTAzMC4yMC4wLjE3MTUzNTEwMzAuMC4wLjA.*_fplc*NVl0RWdzOTd2RkRWTk5OJTJCTkRNN1NlYjhIOE1jRkwzUiUyRllLSE5waWlseGtuS2dQWFBFdzU1SmlXeDRTc3VlelBOWlNnN1clMkZWcm5neXNFJTJGJTJCOXUxSUpURWdrREk1aW14UmcwZ3Y0OCUyRkpmenNvdkkwZXhiJTJCRWhXY282S0lPTnclM0QlM0Q.

# Compartilhar seu projeto

Compartilhe seu codespace com outras pessoas pelo GitHub: https://github.com/
Na página inicial do GitHub, clique no botão "New" (Novo) localizado no canto superior direito;
Preencha o nome do seu repositório e uma breve descrição. Escolha se deseja que o repositório seja público (visível para todos) ou privado (acessível apenas por convite);
Você pode optar por inicializar o repositório com um arquivo README, que é uma boa prática para fornecer informações sobre o projeto. Além disso, você pode escolher uma licença para o seu código, se desejar;
Você pode especificar tipos de arquivos que o Git deve ignorar ao rastrear alterações. Por exemplo, você pode selecionar uma linguagem de programação específica para gerar um arquivo .gitignore correspondente;
Se o seu projeto se encaixa em um dos modelos de projeto disponíveis, você pode escolher um para iniciar com estrutura pré-definida;
Após preencher todas as informações necessárias, clique no botão "Create repository" (Criar repositório) para criar o seu repositório;
Para saber mais confira os primeiros passos no GitHub. https://www.alura.com.br/artigos/o-que-e-git-github?utm_term=&utm_campaign=&utm_source=adwords&utm_medium=ppc&hsa_acc=7964138385&hsa_cam=20946398532&hsa_grp=153091871930&hsa_ad=688089973825&hsa&_gl=1*cqt5nn*_ga*NDY2NTQxMDY5LjE3MTE0MDc0MDQ.*_ga_1EPWSW3PCS*MTcxNTEzNzY3NC4xOC4xLjE3MTUxMzg4OTIuMC4wLjA.*_fplc*cmtMOHI3czklMkJWUDE5R3pMSnBnbUM2cHZVRDNEWDFaUjExQkF0RHdSaFVjNW1mMHVSY0RtQmhEYU8zcW5XTlZnSGlvTVpvd3NqeiUyRkwxN3Rad29EazFCaWlldEtOa205N2tGa2pDSkhoRSUyQkR6ZFhNTlhVQTJtTFJ2WHhmQjB3JTNEJTNE
Divulgue seu projeto
Mostre o seu projeto para o mundo compartilhando no LinkedIn e Instagram! Marque a Alura (@AluraOnline) e o Google (@GoogleBrasil). Vamos adorar ver os seus projetos e acompanhar a sua evolução! Lembre-se de utilizar a hashtag #imersao-ia-alura-google para que o seu projeto alcance ainda mais pessoas.

Estamos ansiosos para mergulhar em aprendizado junto com você! Bom mergulho e até a próxima aula.

> QUEM SÃO OS MERGULHADORES?
> INSTRUTORES E INSTRUTORAS DA ALURA NESSA IMERSÃO

**Fabrício Carraro**
Program Manager e Autor de IA @ Alura
https://twitter.com/fabriciocarraro
https://www.linkedin.com/in/fabriciocarraro/
https://github.com/fabriciocarraro

**Paulo Silveira**
https://cursos.alura.com.br/imersoes/aulas/paulo_caelum
https://www.linkedin.com/in/paulosilveira/

**Ana Raquel**
Cientista de Dados e professora da FIAP
https://www.linkedin.com/in/ana-raquel-fernandes-cunha-a48a07a0/

**Luciano Martins**
Developer Advocate, Google IA.
https://www.linkedin.com/in/lucianommartins/
