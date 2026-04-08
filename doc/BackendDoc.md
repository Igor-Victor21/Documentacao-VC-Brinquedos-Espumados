# Backend

## Visão Geral

O backend é a parte central da aplicação, responsável por toda a lógica do sistema, desde cálculos até a criação, edição, exclusão e visualização de produtos.

Além disso, é onde ocorre a integração com diversas tecnologias, permitindo que toda a aplicação funcione de forma unificada por meio de uma única API.

Atualmente, o sistema já cumpre bem sua principal função de manipulação de dados de produtos. No entanto, ainda há espaço para evolução, com novas funcionalidades sendo planejadas para ampliar as capacidades da aplicação.

Cada nova funcionalidade implementada terá sua própria documentação, que será atualizada conforme o projeto evolui e ganha escala.

No momento, existe uma API principal em funcionamento, e outra API desenvolvida para disponibilizar os produtos em ambiente de testes, permitindo simular o comportamento do sistema completo com todos os dados em produção.

Atualmente, o projeto utiliza plataformas gratuitas para hospedagem, como Render para a API e Vercel para o e-commerce, enquanto o banco de dados já está online e configurado no Firebase.

---

## Arquitetura

O backend do projeto VC Brinquedos Espumados é responsável por centralizar toda a lógica da aplicação, incluindo regras de negócio, segurança, cálculos e integrações com serviços externos.

Toda a comunicação do sistema é feita por meio de uma API REST, que atende as três aplicações principais: e-commerce, dashboard e mobile.

O funcionamento ocorre da seguinte forma:

- O backend recebe requisições das aplicações (frontend, dashboard e mobile)
- A API valida a origem da requisição (URL/domínio) e verifica se ela está autorizada
- Em seguida, realiza as validações de segurança, como autenticação e verificação de permissões

Após essas validações, o comportamento varia conforme a aplicação:

- E-commerce:

  - A API permite apenas a visualização dos produtos
  - Não há acesso a rotas de manipulação de dados

- Dashboard:

  - A API verifica se o usuário está cadastrado
  - Valida o token JWT para autenticação
  - Define o nível de acesso:

    - Administradores possuem acesso completo às funcionalidades
    - Usuários comuns possuem acesso limitado

- Mobile:

  - Segue uma lógica semelhante ao dashboard
  - Permite autenticação do usuário
  - Possui acesso a determinadas funcionalidades de manipulação de dados, conforme o nível de permissão

Essa arquitetura permite que o backend tenha controle total sobre o sistema, garantindo segurança, organização e facilitando a escalabilidade das aplicações.

---

## Tecnologias

Para o desenvolvimento desta API, foram utilizados Node.js e Express, principalmente pela simplicidade e pelo uso da mesma linguagem (JavaScript), o que facilitou o aprendizado e a produtividade da equipe durante o desenvolvimento inicial.

Essas tecnologias permitem uma construção mais rápida e flexível da API, além de serem bem adaptadas para projetos que estão em fase de crescimento e constantes mudanças.

No início do projeto, a escolha por Node.js e Express também foi influenciada pelo foco de estudo da equipe, permitindo aplicar na prática os conhecimentos adquiridos.

Com a possibilidade de crescimento do sistema, já existe um planejamento para migração futura para Spring Boot, visando maior robustez e melhor desempenho em cenários de maior escala. Junto a isso, também está prevista a mudança do banco de dados para MongoDB, buscando maior flexibilidade no armazenamento de dados.

A equipe também pretende evoluir a segurança da aplicação, tanto na API quanto no banco de dados, adotando boas práticas e novas estratégias conforme o sistema cresce.

Atualmente, o projeto ainda está em desenvolvimento e continuará recebendo novas tecnologias e funcionalidades, como agentes de IA, integração com ferramentas de analytics e a evolução da plataforma mobile interna.

---

## Estrutura

### Visão geral da organização do backend:

![BackendEstrutura](../assets/BackendEstrutura.png)

A estrutura do backend foi organizada de forma modular, separando responsabilidades em diferentes pastas e arquivos para manter o código limpo, escalável e de fácil manutenção.

O projeto está dividido da seguinte forma:

- config

  - Responsável pelas configurações de serviços externos, como Cloudinary (imagens) e Firebase (autenticação e banco de dados).

- controllers

  - Contém a lógica principal das funcionalidades da API, como autenticação, gerenciamento de usuários, produtos e área administrativa.

- middlewares

  - Responsáveis por interceptar as requisições antes de chegarem aos controllers.
  - Incluem validações como autenticação (JWT), controle de acesso, proteção contra excesso de requisições (rate limit) e gerenciamento de uploads.

- utils

  - Funções auxiliares reutilizáveis utilizadas em diferentes partes do sistema.

- Arquivos principais

  - app.ts → Configuração principal da aplicação
  - index.ts → Ponto de entrada do servidor
  - routes.ts → Definição das rotas da API
  - mailer.ts → Responsável pelo envio de e-mails

- tmp

  - Utilizado para armazenamentos temporários, como arquivos durante processos internos.

Essa organização permite que cada parte do sistema tenha uma responsabilidade bem definida, facilitando o desenvolvimento em equipe e futuras manutenções.

Por se tratar de uma API privada e de uso interno, alguns detalhes mais específicos da implementação não são expostos nesta documentação.

---

## Segurança

A aplicação conta com diferentes camadas de segurança para garantir a proteção dos dados e o controle de acesso ao sistema:

- Autenticação com Google

  - Permite login seguro utilizando contas Google, reduzindo a necessidade de gerenciamento de senhas e aumentando a confiabilidade da autenticação.

- Token JWT

  - Utilizado para autenticação e autorização das requisições.
  - Garante que apenas usuários autenticados possam acessar rotas protegidas, além de controlar permissões (como acesso administrativo).

- Rate Limiting

  - Protege a API contra excesso de requisições, evitando ataques como força bruta e sobrecarga no servidor.

- CORS

  - Controla quais origens (domínios) podem acessar a API, impedindo requisições não autorizadas de aplicações externas.

- Cookies

  - Utilizados para armazenamento seguro de informações de sessão, auxiliando na autenticação e na persistência de dados do usuário.

---

## Banco de Dados

O banco de dados utilizado no projeto é o Firestore, uma das soluções oferecidas pelo Firebase. A escolha foi feita com base na sua facilidade de uso, rápida configuração e por ser um serviço totalmente gerenciado na nuvem, o que elimina a necessidade de infraestrutura própria.

Além disso, o Firestore já oferece mecanismos de segurança integrados e boa performance para aplicações de pequeno e médio porte, atendendo perfeitamente às necessidades atuais do projeto.

Outro fator relevante na decisão foi a integração com o ecossistema do Firebase, que permite utilizar outras funcionalidades da plataforma de forma simples e eficiente.

No entanto, a equipe está ciente de que, conforme o crescimento do sistema e o aumento no volume de dados e requisições, o Firestore pode apresentar limitações em cenários de alta escala.

Por esse motivo, já existe um planejamento futuro para migração da arquitetura, incluindo a substituição do banco de dados e possíveis ajustes na API, visando maior desempenho, escalabilidade e controle sobre a infraestrutura.

Atualmente, a escolha pelo Firestore está alinhada com o estágio do projeto, garantindo agilidade no desenvolvimento sem comprometer a qualidade e a segurança da aplicação.

---

## Funcionalidades

A API oferece diversas funcionalidades essenciais para o funcionamento das aplicações integradas (web, dashboard e mobile):

- CRUD de Produtos  
  - Permite criar, visualizar, atualizar e remover produtos do sistema.

- CRUD de Usuários  
  - Gerenciamento completo de usuários, incluindo cadastro, edição e exclusão.

- Controle de Permissões  
  - Sistema de alteração de cargos, permitindo elevar usuários comuns para administradores com acesso total ao sistema.

- Upload de Imagens  
  - Integração com o Cloudinary para envio de imagens, retornando a URL otimizada para armazenamento e uso na aplicação.

- Recuperação de Senha  
  - Sistema de redefinição de senha via e-mail, garantindo que o usuário possa recuperar o acesso de forma segura.

---

## Integrações

### Serviços Externos

- Cloudinary  

  - Utilizado para armazenamento de imagens enviadas pelo dashboard, retornando a URL para ser armazenada no banco de dados.

  - A integração foi feita com base na documentação oficial, utilizando testes isolados antes da implementação final.  

  - Essa abordagem permitiu validar o funcionamento do upload e garantir maior segurança antes de integrar diretamente ao fluxo principal da aplicação.

---

### E-commerce

A integração com o e-commerce foi projetada de forma simples, sendo responsável apenas pela visualização dos produtos.  

O backend expõe rotas controladas, permitindo apenas requisições de leitura.  
Essa decisão reduz a complexidade e aumenta a segurança, evitando que o e-commerce tenha acesso a operações sensíveis.

---

### Dashboard

A integração com o dashboard é a mais completa, sendo responsável pelo consumo das principais funcionalidades da API. 

O processo envolveu a conexão de múltiplos endpoints, incluindo autenticação, CRUD e controle de permissões.  

Devido à quantidade de funcionalidades, foi necessário um cuidado maior com validações, organização das rotas e segurança da aplicação.  

Essa integração representa o principal ponto de gerenciamento do sistema.

---

### Mobile

A integração com o mobile foi realizada utilizando Expo React Native, aproveitando a similaridade com o ecossistema React. 

O desenvolvimento ocorreu após a consolidação do backend e do dashboard, permitindo reutilizar padrões já definidos.  

Apesar da base semelhante ao frontend web, foram necessárias adaptações específicas para o ambiente mobile. 

Essa abordagem facilitou a implementação e manteve consistência entre as aplicações.

---
## Deploy

O deploy do backend encontra-se temporariamente suspenso, pois o sistema ainda está em fase de testes e validações internas.

- API separada para testes
- Planejamento de deploy em VPS
- Foco em performance e estabilidade

---

## Melhorias Futuras

- Agentes de IA
- Analytics de Produtos
- Funil de Vendas

### Infraestrutura

- Migração para Spring Boot
- Migração para MongoDB
- Reforço de segurança

---

## Observações

A API está em constante evolução, buscando sempre incorporar novas tecnologias para otimizar os processos e o tempo da empresa.

Além disso, trata-se de uma API totalmente privada e de uso interno, não sendo disponibilizada publicamente.
