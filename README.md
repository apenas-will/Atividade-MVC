# Nome do Projeto: Abandono Zero

## Descrição:

O projeto consiste em uma aplicação web realizada em parceria com o [INSPA](https://psicologiaanimal.com.br/), uma empresa especializada no ensino de psicologia animal, que coleta dados do usuário por meio de um formulário. O objetivo final é a criação de uma base de dados que permita posteriores analises dos perfis desses usuários e como estes estão relacionados ao comportamento de compra, adoção e/ou abandono de animais.

A aplicação dispõe de páginas para login e cadastro, além daquelas responsáveis por apresentar os dados a usuários autorizados e a do próprio formulário.

### Arquitetura:

O modelo de arquitetura utilizado foi o MVC (Model-View-Controller), o qual divide uma aplicação web em estruturas com funções específicas.

### Ferramenta de Diagramação:

Para a diagramação do esquema da arquitetura foi utilizado a ferramenta [Draw.io](https://www.drawio.com/).

## Modelos (Models):

Descreva as entidades do seu projeto e seus atributos.

Explique as relações entre as entidades.

A camada de Models é responsável por interagir diretamente com o banco de dados, estabelecendo como os dados são armazenados e recuperados. [[1]](#referências-bibliográficas)

Como supracitados diferentes entidades contidas nesta camada representam como os dados estão organizados dentro do banco de dados, estruturando-os em tabelas com atributos distintos. Nos Quadros 1 a 4, pode-se observar algumas das entidades dessa camada, suas relações e seus atributos.

<div align="center">
<sub align="center">Quadro 1 - Model user </sub>

|  Característica   | Descrição |
| :--------------- | :------- |
| Responsabilidade  |    Estabelecer como devem ser armazenados dados dos usuários cadastrados, como email, nome, senha e o papel que ele exerce na aplicação (o que determina as funções que ele tem acesso).        |
| Controllers conectados  |   "User"        |
| Models conectados |  Conectado a todos os módulos, fornecendo uma _primary key_ chamada "id".    |
|      Atributos      | **id**: Atribuido automáticamente, serve como um identificador universal do usuário, eliminando conflitos que possam ser causados por pessoas com mesmo nome.  <br> **nome**: Armazena o nome do usuário no momento do cadastro <br> **email**: Armazena o email do usuário no momento do cadastro <br> **senha**: Armazena a senha do usuário de maneira criptografada <br> **role**: Determina o "papel" do usuário na aplicação, definindo as informações que ele terá acesso na aplicação.     |

<sup> Fonte: Material produzido pelo autor, 2024<sup>
</div>

<div align="center">
<sub align="center">Quadro 2 - Model resenha </sub>

|  Característica   | Descrição |
| :--------------- | :------- |
| Responsabilidade  |    Estabelecer como devem ser armazenados as respostas inseridos pelo usuário no formulário de resenha.        |
| Controllers conectados  |   "forms" e "dashboard"        |
| Models conectados |  "user"    |
|      Atributos      | **id**: Atribuido automáticamente, serve como um identificador do usuário dentro do model. <br> **user_id**: _Foreign key_ vinda do model "user". Por meio deste atributo, pode-se relacionar as informações contidas neste model com àquelas que estão no _user_.  <br> **nome**: Armazena o nome inserido no formulário de resenha. <br> **email**: Armazena o email inserido no formulário de resenha. <br> **idade**: Armazena a idade inserida no formulário de resenha. <br> **sexo**: Armazena o sexo inserido no formulário de resenha. <br> **escolaridade**: Armazena o grau de escolaridade inserido no formulário de resenha. <br> ***Outros atributos estão presentes neste model, cada um relativo a uma pergunta do formulário de resenha**. [[2]](#referências-bibliográficas)  |

<sup> Fonte: Material produzido pelo autor, 2024<sup>
</div>

<div align="center">
<sub align="center">Quadro 3 - Model tem_cão </sub>

|  Característica   | Descrição |
| :--------------- | :------- |
| Responsabilidade  |    Estabelecer como devem ser armazenados as respostas inseridos pelo usuário no formulário destinado a pessoas que tenham cães.        |
| Controllers conectados  |   "forms" e "dashboard"        |
| Models conectados |  "user"    |
|      Atributos      | **id**: Atribuido automáticamente, serve como um identificador do usuário dentro do model. <br> **user_id**: _Foreign key_ vinda do model "user". Por meio deste atributo, pode-se relacionar as informações contidas neste model com àquelas que estão no _user_. <br> **nome do cão**: Armazena o nome do cão inserido no formulário destinado a pessoas que tem cães. <br> **número de pets**: Armazena o número de pets do usuário inserido no formulário destinado a pessoas que tem cães. <br> **idade**: Armazena a idade do cão inserido no formulário destinado a pessoas que tem cães. <br> **raça**: Armazena a raça do cão inserido no formulário destinado a pessoas que tem cães.<br> ***Outros atributos estão presentes neste model, cada um relativo a uma pergunta do formulário de "Quem tem cão"**. [[2]](#referências-bibliográficas)  |

<sup> Fonte: Material produzido pelo autor, 2024<sup>
</div>

<div align="center">
<sub align="center">Quadro 4 - Model quer_ter </sub>

|  Característica   | Descrição |
| :--------------- | :------- |
| Responsabilidade  |    Estabelecer como devem ser armazenados as respostas inseridos pelo usuário no formulário destinado a pessoas que querem ter cães.        |
| Controllers conectados  |   "forms" e "dashboard"        |
| Models conectados |  "user"    |
|      Atributos      | **id**: Atribuido automáticamente, serve como um identificador do usuário dentro do model. <br> **user_id**: _Foreign key_ vinda do model "user". Por meio deste atributo, pode-se relacionar as informações contidas neste model com àquelas que estão no _user_. **"Perguntas"**: Representa a informação que será armazenada pelo formulário, sendo relativa as perguntas que ainda serão disponibilizadas.  |

<sup> Fonte: Material produzido pelo autor, 2024<sup>
</div>

## Controladores (Controllers):

Os Controladores, ou _Controllers_, são responsáveis por intermediar as interações da camada de visualização e, portanto, os comandos do usuário, com a camada que trata dos dados. [[1]](#referências-bibliográficas)

Nesse sentido, estão listados os _Controllers_ da arquitetura, juntamente com as outras entidades com qual interagem, suas responsabilidades, métodos e parâmetros de entrada e saída (Quadros 5 a 7).

<div align="center">
<sub align="center">Quadro 5 - Controller User </sub>

|  Característica   | Descrição |
| :--------------- | :------- |
| Responsabilidade  |    Estabelecer a conexão das páginas de login e cadastro com o Model de "User", permitindo que sejam gravadas informações e que possam ser averiguados dados pontuais       |
| Views conectadas  |   "Página de login" e "Página de cadastro"        |
| Models conectados |       "User"    |
|      Methods      |  **Gravar**: Insere informações no banco de dados, tomando como entrada valores alfanuméricos. <br> **Procurar**: Busca informações pontuais, nesse caso específico, é usado para averiguar se a senha está de acordo com a registrada na página de login, retornando um valor booleano.    |

<sup> Fonte: Material produzido pelo autor, 2024<sup>
</div>

<div align="center">
<sub align="div">Quadro 6 - Controller Forms </sub>

|  Característica   | Descrição |
| :--------------- | :------- |
| Responsabilidade  |    Estabelecer a conexão das várias páginas do formulário com os seus respectivos Models, permitindo que sejam gravadas informações de maneira organizada para consultas posteriores       |
| Views conectadas  |   Páginas dos formulários        |
| Models conectados |       Todas as Models relativas ao formulário, como a "resenha", "tem_cão", "quer_ter" etc.     |
|      Methods      |  **Gravar**: Insere informações no banco de dados, tomando como entrada valores alfanuméricos |

<sup> Fonte: Material produzido pelo autor, 2024<sup>
</div>

<div align="center">
<sub align="center">Quadro 7 - Controller Dashboard </sub>

|  Característica   | Descrição |
| :--------------- | :------- |
| Responsabilidade  |    Estabelecer a conexão da página de dashboard com os diversos Models, permitindo que sejam lidas informações do banco de dados e gerar gráficos e tabelas a partir delas       |
| Views conectadas  |   "Dashboard do adm"        |
| Models conectados |       Todas as Models relativas ao formulário, como a "resenha", "tem_cão", "quer_ter" etc.     |
|      Methods      |  **Procurar**: Busca por informações pontuais, as apresentando diretamente na forma de valores alfanuméricos. <br> **Listar**: Lista várias informações que atendem a um critério, retornando valores alfanuméricos que pode ser convertidos em gráficos e/ou tabelas.|

<sup> Fonte: Material produzido pelo autor, 2024<sup>
</div>

## Views (Views):

As _Views_ dizem respeito a parte visual do projeto, mais especificamente a parte visível ao usuário.

Nesse sentido, o projeto apresenta uma série de _Views_ que representam as diversas telas com as quais o usuário pode interagir, e que, por sua vez, têm acesso ao controles para interagir com a camada de _Model_. [[1]](#referências-bibliográficas)

No Quadro 8, estão listadas as _Views_ do projeto com suas respectivas funções:

<div align="center">
<sub align="center">Quadro 8 - Views </sub>

|            View            |                                                 Função                                                 |
| :------------------------ | :---------------------------------------------------------------------------------------------------- |
|      Página de login       |                  Realizar o login do usuário, averiguando o email e senha inseridos.                   |
|     Página de cadastro     | Realizar o cadastro de um novo usuário, coletando dados como email, nome e senha, confirmando a senha. |
|   Páginas do formulário    |      Apresentar as perguntas dos diferentes formulários e coletar as respostas dessas perguntas.       |
| Dashboard do administrador |  Apresentar os dados presentes no banco de dados de forma visual e permitir o download desses dados.   |
| Página inicial |  Apresentar informações gerais sobre o projeto e direcionar o usuário para a página de login.   |

<sup> Fonte: Material produzido pelo autor, 2024<sup>
</div>

## Infraestrutura:

Os diferentes elementos do diagrama MVC se integram em diversas instâncias dentro da aplicação. 

A priori, temos acesso ao servidor por meio do serviço [Render](https://render.com/). Além disso, é utilizado o banco de dados [Postgre](https://www.postgresql.org/), acessando esse banco de dados por meio do servidor de banco de dados do Render.

Por fim, também emprega-se o _framework_ [Sails.js](https://sailsjs.com/), o qual tem grande participação ao simplificar o processo de desenvolvimento da aplicação.

## Justifique as escolhas feitas e como elas impactam o projeto.

### Implicações da Arquitetura:

A várias escolhas relacionadas à construção do digrama MVC apresentam diversas consequências e implicações. Em um primeiro momento, a utilização de um banco de dados relacional permite que o acesso às informações de maneira organizada, além de possibilitar que sejam estabelecidas relações entre as informações de maneira simplificada.

A escolha por separar os _Models_ de cada formulário, ao invés de unificá-los, visou a escalabilidade, permitindo que novos perfis e formulários pudessem ser inseridos na aplicação sem afetar a integridade de outras informações. Nesse sentido, utilizou-se uma _foreign key_ proveniente do modelo "user" para estabelecer a conexão entre as tabelas. A separação dos modelos também auxilia na sua manutenção, visto que pode-se alterar uma delas sem impactar as outras.

## Referências bibliográficas
1. ALVES, William Pereira. Java para Web: desenvolvimento de aplicações. São Paulo: Erica, 2015. 1 recurso online. ISBN 9788536519357. Disponível em: https://integrada.minhabiblioteca.com.br/books/9788536519357. Acesso em: 26 abr. 2024.
2. INSPA. Base questionário abandonozero Q1. 2024. Disponível em: https://inteli-college.slack.com/files/U049107B7MZ/F06V33D6LNQ/base_question__rio__abandonozero__q1_-_inteli__e_inspa.pdf. Acesso em: 26 abr. 2024.