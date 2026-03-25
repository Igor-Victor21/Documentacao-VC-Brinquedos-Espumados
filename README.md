# Documentação VC Brinquedos Espumados

![HeaderDocumentation](./assets/Header%20documentation.jpg)

---

# Visão Geral do Projeto

Este projeto consiste no desenvolvimento de um sistema completo de e-commerce, voltado para facilitar o gerenciamento, a catalogação e a exibição de produtos.

A solução também tem como foco otimizar o atendimento ao cliente, proporcionando mais eficiência, organização e praticidade tanto para os usuários quanto para a equipe interna.

---

## Objetivo

O objetivo principal desta aplicação é o desenvolvimento de um sistema de e-commerce que permita o gerenciamento de produtos por meio de um dashboard administrativo, além de contar com sistemas estruturados, rotas bem definidas e mecanismos de segurança, como autenticação baseada em tokens e controle de requisições.

Atualmente, o objetivo inicial já se encontra implementado e funcional. A próxima etapa do projeto consiste na evolução da aplicação, com a inclusão de um agente de IA voltado para vendas, bem como a implementação de um sistema de analytics, permitindo que a equipe interna acompanhe e otimize o funil de vendas de forma mais estratégica.

## Funcionalidades

- Autenticação de usuários com integração ao Google

- Sistema de autenticação e autorização utilizando tokens JWT

- Implementação de rate limiting para controle de requisições e maior segurança da aplicação

- CRUD completo de produtos por meio de um dashboard administrativo

- Comunicação estruturada entre front-end e back-end via API

- Armazenamento e gerenciamento de imagens de produtos utilizando o Cloudinary

- Agente de IA voltado para vendas (em desenvolvimento)

- Sistema de analytics para acompanhamento do funil de vendas (em desenvolvimento)

---

## Tecnologias Utilizadas

### Linguagem
- JavaScript / TypeScript

---

## Frontend

### E-commerce
- Next.js
- Tailwind CSS  

[Saiba mais](./doc/E-commerceDoc.md)

### Dashboard
- React
- Vite  

[Saiba mais](./doc/DashboardDoc.md)

### Mobile
- React Native  

[Saiba mais](./doc/MobileDoc.md)

---

## Backend
- Node.js
- Express
- API REST
- JWT (JSON Web Token)  

[Saiba mais](./doc/BackendDoc.md)

---

## Banco de Dados
- Firebase / Firestore  

[Saiba mais](./doc/DatabaseDoc.md)

---

## Serviços Externos
- Cloudinary  

[Saiba mais](./doc/ServicosExternos.md)

---

# Arquitetura e Estrutura

## Arquitetura

O projeto VC Brinquedos Espumados funciona, de forma geral, por meio de uma API REST. Toda a lógica de negócio, segurança, cálculos e integrações com serviços externos é centralizada no backend, garantindo maior controle e segurança da aplicação.

A comunicação entre as partes do sistema ocorre da seguinte forma:

- O front-end realiza requisições para a API
- A API valida a origem da requisição (URL/domínio)
- Caso a requisição esteja autorizada:

  - No E-commerce: é permitido apenas visualizar os produtos
  - No Dashboard: o acesso é restrito a administradores para gerenciamento de produtos, usuários comuns possuem apenas permissão de visualização
  - No Mobile: segue a mesma lógica do dashboard (até o momento)

Essa estrutura permite maior organização, controle de acesso e escalabilidade do sistema.

---

## Estrutura

A estrutura das três aplicações está organizada por meio de pastas bem definidas, incluindo separação para componentes visuais, imagens e documentação interna do projeto.

Essa organização segue um padrão consistente, facilitando a manutenção, futuras modificações e a inclusão de novas funcionalidades.

Além disso, a padronização do projeto permite que outros desenvolvedores consigam entender e trabalhar no código com mais facilidade, seja para ajustes ou para a adição de novas tecnologias.

---

# Integrações (APIs e Serviços)

O projeto possui uma API própria, responsável por toda a lógica da aplicação. Além disso, conta com integração com o Cloudinary para o gerenciamento de imagens dos produtos.

Por meio dessa integração, é possível realizar o upload, edição e exclusão de imagens, mantendo os arquivos organizados externamente e evitando o acúmulo de mídia dentro do sistema.

### Futuras adições

- Integração com API REST do n8n, para implementação de agentes de IA
- Integração com WhatsApp Business Platform, para automatização do atendimento ao cliente

---

# Desafios Enfrentados

Um dos principais desafios do projeto foi a transição do banco de dados relacional (SQL Server), com o qual já havia familiaridade, para o uso do Firebase (Firestore), que possui uma abordagem NoSQL.

Essa mudança exigiu adaptação a uma nova forma de estruturar e consultar os dados, além de apresentar dificuldades na integração com a API, principalmente por conta das diferentes formas de conexão e manipulação do banco.

Durante aproximadamente um mês, foram realizados diversos testes e ajustes até que a comunicação entre a aplicação e o banco de dados estivesse funcionando de forma estável.

Também foram enfrentados problemas relacionados à conexão e à autenticação do Firebase. No entanto, após testes adicionais e validações em projetos separados, foi possível corrigir esses pontos e garantir o funcionamento adequado do sistema.

Apesar dos desafios, essas situações contribuíram diretamente para o aprofundamento do conhecimento em integração de APIs, bancos de dados NoSQL e autenticação em aplicações modernas.

---

# Melhorias Futuras

As próximas evoluções do projeto têm como foco ampliar a automação, a inteligência do sistema e o suporte à tomada de decisões.

- Implementação de agentes de IA, com foco em atendimento e suporte ao cliente
- Automação de processos de atendimento e vendas, visando maior eficiência e redução de tarefas manuais
- Desenvolvimento de um sistema de analytics, permitindo o acompanhamento de métricas e otimização do funil de vendas

---

# Aprendizados

Durante o desenvolvimento deste projeto, foram adquiridos diversos aprendizados, envolvendo tanto aspectos técnicos quanto organizacionais.

Entre os principais pontos, destacam-se o aprofundamento no uso de tecnologias, práticas de design UI/UX, levantamento de requisitos e organização de projetos.

Além disso, houve evolução em conceitos relacionados a DevOps e ao ciclo completo de desenvolvimento, abrangendo desde a construção até a estruturação e manutenção da aplicação.

Mesmo em áreas nas quais a equipe já possuía conhecimento, o projeto serviu como uma oportunidade para aperfeiçoar habilidades e tornar as soluções ainda mais consistentes e bem estruturadas.

---

# Segurança

O sistema de segurança desenvolvido atualmente é sólido e adequado para o porte do projeto, garantindo proteção e controle de acesso às funcionalidades da aplicação.

Entre os principais mecanismos implementados, destacam-se:

- Configuração de CORS, permitindo o acesso apenas a URLs autorizadas
- Autenticação de usuários com integração ao Google
- Utilização de tokens JWT para autenticação e controle de sessões
- Proteção de rotas privadas, exigindo token válido para acesso
- Implementação de rate limiting para evitar requisições abusivas e possíveis ataques
- Sistema de controle de permissões de usuários (ex: administrador e usuário comum)

O projeto VC Brinquedos Espumados ainda está em fase inicial e, conforme evoluir, tanto a aplicação quanto os mecanismos de segurança serão aprimorados de forma contínua.

Atualmente, o sistema já se encontra funcional e seguro para o seu contexto, com possibilidade de futuras melhorias e reforços na camada de segurança.

---

# Deploy

O projeto está planejado para ser hospedado em um serviço de VPS. No momento, a aplicação ainda não se encontra em produção, pois está em fase de desenvolvimento, com novas funcionalidades sendo implementadas.

Além disso, o deploy definitivo depende da disponibilização de recursos financeiros por parte da empresa responsável pelo projeto.

Assim que essas etapas forem concluídas, a aplicação será publicada e disponibilizada para acesso.

---

# Autor

Desenvolvido por:

- Igor Victor  
  GitHub: https://github.com/Igor-Victor21

- Vinicius Koujaki  
  GitHub: https://github.com/Vinicius-Koujaki-Nobre

- Fabio Luis  
  GitHub: https://github.com/roottracker

- Jaqueline Batista  
  GitHub: https://github.com/KiriNagsCloud

---

# 🔒 Status do Projeto

Atualmente este projeto encontra-se em ambiente privado para fins de desenvolvimento e validação.

A publicação e disponibilização pública será realizada após a finalização das funcionalidades principais e ajustes finais.
