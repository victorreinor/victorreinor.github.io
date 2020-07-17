---
title: "O que é NodeJs?"
published: true
---
- Node foi construido em cima da engine V8 que interpreta Javascript, criado pela Google e usado em seu navegador Chrome
- Nodejs é mais conhecido como **Uma plataforma para construir aplicações web escaláveis de alta performance usando JavaScript**

##### Node não e um servidor web!
- Isso mesmo node não e um servidor web, de um jeito grosseiro o nodejs permite que escreva javascript no seu computador, com uma arquitetura voltada a eventos. Requisições com nodejs é feita de forma assicrona com funções de callback, em vez de sequencial, tornando rápido para lidar com um número muito alto de requisições.

##### 'Beleza, então como eu crio aplicacoes web com nodejs?'
- Bem simples, você deverá criar um servidor web em cima do nodejs, ou seja, em javascript. **Mais a baixo iremos demonstar como criar um servidor web simples com o nodejs.**
- Eu costumo falar que o nodejs é uma maquina de frameworks/bibliotecas de javascript pois ele facilita muito na hora de instalação, facilidade de procura ou criação, rapidez, facil de usar, entre muitas outras coisas mais.  Juntamente com o node temos o NPM, que seria: Node package module (Gerenciador de pacotes), ou seja, ele permite que voce instale pacotes no seu projeto nodejs ([Site Npm](https://www.npmjs.com/ "Site Npm")).

##### 'Existem outros tipos de gerenciador de pacotes?'
- Sim, não temos somente o npm como gerenciador de pacotes voce pode instalar outros tipo como o yarn ([Site Yarn](https://yarnpkg.com/pt-BR/ "Site Yarn")), que seria um gerenciador de pacotes do facebook com colaboração das empresas Google, Exponent e Tilde, dizem ser mais rapido e seguro que o npm 🤔🤔...

##### Abaixo alguns exemplos de aplicações que são feitas com nodejs:
 - Apis,
 - Aplicações web real-time com servidores de chat ou aplicações colaborativas entre multiplos usuarios,
 - Jogos multiplayer,
 - Aplicacoes que demamdan alta escabilidade,
 - Servidores de streaming de dados;

#### Como instalar o NodeJs
Entre no site oficial https://nodejs.org/ e faça o download e o instale, para saber se foi instalado com sucesso abra o prompt de comando e digite o seguinte comando
`node -v` (retornará a versão que foi instalada do node)
Em seguida digite o comando
`npm -v` (retornará a versão que foi instalada do npm)

#### Exemplo de um servidor web com nodejs
Pronto, agora crie uma pasta e logo em seguida crie um arquivo chamado servidor.js e escreva o seguinte código

```javascript
const http = require('http');
const host = '127.0.0.1';
const port = '3000';
  
const server = http.createServer(function(req, res) {

})
```
O começo indica as variáveis que o nosso servidor irá usar.

Require **require('http')**  é a forma do Node.js carregar seus módulos, neste caso carregamos o modulo http que contém as funções para criar o servidor.  Em seguida é criado o servidor em si, colocando-o em uma variável chamada server. Ainda criamos um callback para cada requisição recebida. Mas ele ainda não faz nada! Vamos continuar:

```javascript
const http = require('http');
const host = '127.0.0.1';
const port = '3000';
 
const server = http.createServer(function(req, res) {
	res.writeHead(200, {'Content-Type': 'text/html; charset=utf-8'});
    res.end("<h1>Olá mundo! Experimentando Node.js</h1>");
}).listen(port, host, function() {
  console.log('Servidor rodando em http://' + host + ':' + port);
});
```
No caso, res é a variável que indica a nossa resposta que iremos enviar ao usuário. Com ela, definimos no header, com writeHead, que a requisição foi um sucesso (código 200) e o tipo do conteúdo da resposta. Depois, enviamos para o usuário um html com a nossa mensagem.

No final, a função listen é usada para receber as requisições no endereço e na porta definidas com as nossas variáveis, quando feito isso, irá chamar uma outra callback e logar uma mensagem interna.

E é isso, você acaba de implementar seu primeiro servidor de Node.js!

Para ver o seu trabalho, vá até a pasta onde você criou o arquivo e no terminal execute:

`node servidor.js`

Você deve ver a mensagem que definimos no prompt, depois disso é só abrir o seu navegador e digitar http://localhost:3000/;

---------

Parar criar um projeto no nodejs utilize o comando
`npm init`

E em seguida aparecerá várias perguntas na tela:
 - Package name (Aqui será o nome do seu projeto): teste-nodejs
 - Version (Aqui será colocado a versão do seu projeto) : Enter para ignorar caso queire
 - Description (Coloque uma descricao do seu projeto): Enter para ignorar caso queire
 - Test commando (Comando para testar o seu projeto): Enter para ignorar caso queire
 - Git repository (Repositorio do git): Enter para ignorar caso queire
 - keywords (palavras-chave do seu projeto): Enter para ignorar caso queire
 - autho ( Autor do projeto ): Enter para ignorar caso queire
 - License ( Tipo da licensa do projeto) : Enter para ignorar caso queire e enfim a ultima pergunta "is this ok? (yes)" digite 'yes' para confirmar
 
**Caso queire ignorar todas essas perguntas e criar o projeto com apenas um comando, digite:**
`npm init -y`

Segue abaixo o link para documentacao do npm:
https://docs.npmjs.com/

#### Obs: Estamos utilizando o node sem pacotes nenhum, existe N maneiras de criar um servidor web como por exemplo com o pacote Express que em poucas linhas criamos um servidor web com muita mais funcoes e muito mais eficaz

###### fonte: [Link 1](https://tableless.com.br/o-que-nodejs-primeiros-passos-com-node-js/ "Link 1"), [Link 2](https://medium.com/thdesenvolvedores/node-js-o-que-%C3%A9-por-que-usar-e-primeiros-passos-1118f771b889 "Link 2"), [Link 3](https://pt.stackoverflow.com/questions/149296/pra-que-server-o-expressjs "Link 3")

