# Banco de Dados (Firestore)

## Visão Geral

O banco de dados foi uma das principais dúvidas da equipe no momento de decidir qual tecnologia utilizar para a aplicação. Após análise, foi escolhido o Firestore, principalmente por fazer parte do ecossistema do Firebase.

O Firebase disponibiliza diversas funcionalidades em uma única plataforma, muitas delas gratuitas, além de possuir uma documentação bem completa e bastante conteúdo disponível na internet. Isso facilitou o processo de desenvolvimento e ajudou a equipe a economizar tempo, já que não foi necessário implementar várias soluções separadamente.

Outro ponto importante foi a segurança, já que se trata de uma plataforma gerenciada pelo Google, trazendo mais confiabilidade para o projeto.

Com isso, o Firestore se encaixou bem no propósito da aplicação, que é um sistema de e-commerce de pequeno a médio porte, permitindo gerenciar produtos de forma simples, organizada e eficiente.

Utilizando o Firebase, foi possível centralizar funcionalidades importantes como banco de dados, autenticação e segurança em um único ambiente, trazendo mais praticidade para o desenvolvimento e manutenção do sistema.

--- 

## Estrutura do Banco

Em relação à estrutura do banco de dados, o Firestore oferece uma organização baseada em coleções e documentos, o que torna o gerenciamento dos dados mais simples e intuitivo.

Atualmente, o sistema possui uma coleção principal de produtos, onde todos os dados relacionados aos produtos estão armazenados e organizados de forma padronizada dentro da própria plataforma.

Em relação aos usuários, o gerenciamento é feito diretamente pelo sistema de autenticação do Firebase. A plataforma já oferece uma área própria para controle de usuários, permitindo que o administrador realize ações como cadastro e redefinição de senha de forma manual.

Por esse motivo, não foi necessário criar uma coleção específica para armazenar e-mails e senhas dentro do banco de dados, já que essa responsabilidade é tratada pelo próprio Firebase de forma segura.

Essa abordagem facilita a manutenção do sistema, reduz a complexidade da aplicação e torna mais simples a integração entre o banco de dados e a API, além de contribuir para uma melhor configuração das regras de segurança.

---

## Modelagem de Dados

A modelagem de dados foi estruturada utilizando o padrão de coleções e documentos do Firestore, mantendo uma abordagem simples e eficiente para o tipo de aplicação.

Foi definida uma coleção principal para produtos, onde cada documento representa um produto individual com seus respectivos atributos. Essa abordagem evita complexidade desnecessária e facilita tanto a leitura quanto a escrita dos dados.

Os dados foram organizados de forma direta dentro de cada documento, sem uso de documentos aninhados, priorizando performance e simplicidade nas consultas, já que a aplicação trabalha principalmente com leitura de produtos.

Alguns campos podem assumir valores nulos (como diâmetro, por exemplo), permitindo flexibilidade para diferentes tipos de produtos sem a necessidade de múltiplas estruturas.

Essa modelagem foi escolhida pensando em:

- Facilidade de manutenção  
- Baixa complexidade nas consultas  
- Boa performance para leitura de dados  
- Facilidade de integração com o backend  

---

## Coleções

Atualmente, o banco de dados possui uma coleção principal responsável pelo funcionamento da aplicação.

---

### Usuários

O gerenciamento de usuários não é feito diretamente por uma coleção no Firestore.

A autenticação e controle de usuários são realizados pelo Firebase Authentication, que já oferece uma estrutura própria para:

- Login  
- Cadastro  
- Redefinição de senha  
- Gerenciamento de contas  

Com isso, não foi necessário criar uma coleção específica para armazenar dados sensíveis como e-mail e senha, aumentando a segurança e reduzindo a complexidade do sistema.

Informações como permissões (admin ou usuário comum) são tratadas via backend e validações com token JWT.

---

### Produtos

A coleção `products` é a principal do sistema, responsável por armazenar todas as informações necessárias para exibição e manipulação dos produtos.

Cada documento dentro dessa coleção representa um produto e contém os seguintes campos:

- name  
  - Nome do produto exibido no sistema  

- description  
  - Descrição detalhada do produto  

- price  
  - Valor do produto  

- discount  
  - Percentual de desconto aplicado  

- imageUrl  
  - URL da imagem armazenada no Cloudinary  

- imagePublicId  
  - Identificador da imagem no Cloudinary (utilizado para edição e exclusão)  

- createdAt  
  - Data de criação do produto  

- section  
  - Categoria ou seção do produto (ex: "todos, desconto, playground etc...")  

- height  
  - Altura do produto  

- width  
  - Largura do produto  

- length  
  - Comprimento do produto  

- diameter  
  - Diâmetro do produto (pode ser nulo dependendo do tipo)  

Essa estrutura permite flexibilidade para diferentes tipos de produtos, mantendo um padrão único de dados e facilitando tanto a exibição no frontend quanto a manipulação via dashboard.

---
## Regras de Segurança

As regras de segurança do banco de dados foram definidas com base no tipo de acesso de cada aplicação integrada ao sistema, garantindo controle sobre leitura e manipulação de dados.

No e-commerce, o acesso é restrito apenas à visualização dos produtos, não sendo permitido realizar qualquer tipo de modificação nos dados. Essa abordagem reduz riscos e mantém a integridade das informações exibidas ao cliente.

No dashboard, o acesso é controlado por níveis de permissão:

- Usuários comuns possuem acesso apenas para visualização dos dados  
- Administradores possuem acesso completo, podendo realizar operações de criação, edição e exclusão (CRUD)  

Toda a validação de permissões é realizada em conjunto com o backend, utilizando autenticação via Token JWT e verificação de nível de acesso do usuário.

Essa estrutura garante que apenas usuários autorizados possam realizar alterações no sistema, mantendo a segurança e o controle sobre os dados.

---

## Integração com o Backend

A integração entre o backend e o Firestore é realizada de forma centralizada através da API desenvolvida em Node.js com Express.

O backend é responsável por toda a comunicação com o banco de dados, sendo o único ponto que realiza leitura e escrita diretamente no Firestore. Dessa forma, as aplicações (e-commerce, dashboard e mobile) não acessam o banco diretamente, garantindo maior controle e segurança.

A conexão com o Firestore é feita utilizando o SDK oficial do Firebase, configurado na camada de `config` do projeto. A partir dessa configuração, os controllers utilizam funções específicas para realizar operações como:

- Consulta de produtos  
- Criação de novos registros  
- Atualização de dados  
- Remoção de documentos  

As requisições seguem o padrão REST, onde cada rota definida no backend é responsável por uma ação específica no banco de dados.

Além disso, a integração foi estruturada com foco em segurança, utilizando:

- Validação de autenticação via Token JWT  
- Controle de permissões por nível de usuário  
- Interceptação de requisições por middlewares  

Essa abordagem garante que todas as operações no banco sejam controladas, evitando acessos diretos e mantendo a organização da aplicação.

---

## Performance e Escalabilidade

A estrutura do Firestore foi utilizada de forma simples e eficiente, priorizando performance em operações de leitura, que são as mais utilizadas no sistema.

Como os dados estão organizados em uma única coleção principal (`products`), as consultas são diretas e rápidas, sem necessidade de operações complexas ou junções, o que favorece o desempenho.

Boas práticas adotadas:

- Estrutura de documentos simples e padronizada  
- Evitar dados aninhados desnecessários  
- Uso de campos diretos para facilitar buscas  
- Separação de responsabilidades via backend  

O Firestore, por ser um banco NoSQL gerenciado, já oferece escalabilidade automática, suportando aumento de requisições sem necessidade de configuração manual de infraestrutura.

Para o contexto atual do projeto (pequeno a médio porte), o desempenho atende completamente as necessidades, mantendo respostas rápidas e estabilidade.

---

## Limitações

Apesar das vantagens, o uso do Firestore apresenta algumas limitações que foram consideradas durante o desenvolvimento:

- Dificuldade em consultas mais complexas, por não utilizar modelo relacional  
- Limitações em filtros avançados e combinações de consultas  
- Dependência de estrutura bem planejada para evitar retrabalho  
- Possíveis custos elevados em larga escala, dependendo do volume de leitura e escrita  

Além disso, para aplicações de grande porte com alto volume de dados e regras complexas, o Firestore pode não ser a melhor opção a longo prazo.

---

## Melhorias Futuras

Com o crescimento do projeto, algumas melhorias já estão planejadas para evolução do banco de dados:

- Reestruturação da modelagem de dados, caso surjam novas necessidades  
- Otimização de consultas e organização de campos para melhorar performance  
- Implementação de regras de segurança mais avançadas no Firebase  

### Infraestrutura

- Possível migração para banco de dados como MongoDB  
- Ajustes na API para suportar maior volume de requisições  
- Evolução da arquitetura para suportar escalabilidade maior  

Essas melhorias visam preparar o sistema para cenários de maior escala, mantendo desempenho, segurança e organização.

---

## Observações

O banco de dados faz parte de uma estrutura interna da empresa, portanto algumas informações não podem ser disponibilizadas nesta documentação por questões de segurança.

Além disso, existem estudos e planejamentos para utilização de outros tipos de banco de dados no futuro, que ainda estão em fase de discussão pela equipe.

Dessa forma, o projeto como um todo é privado, sendo disponibilizada apenas a documentação previamente revisada e autorizada pela própria empresa.

---