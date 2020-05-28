---
title: "O que é Webpack?"
published: true
---
[![Webpack](http://webpack.github.io/assets/what-is-webpack.png "Webpack")](http://webpack.github.io/assets/what-is-webpack.png "Webpack")

**O que o webpack é capaz de fazer?**
------------

- **Bundle:** Verifica os imports da sua aplicação e agrupa (bundle) tudo em um arquivo só de forma modularizada. Ele faz isso para javascript e seus derivados (typescript, coffeescript e etc...), para css (less, sass e etc...) e imagens. **Conforme a imagem acima**

- **Minify:** Ele diminui seu arquivo de bundle, ou seja, ele pega todo seu código do arquivo bundle e junta tudo em uma linha só, assim diminuindo o tamanho do arquivo, muito utilizado por causa da velocidade de upload e velocidade de carregamento do site

- **Transpiler:** Pega arquivos que nao sao legiveis no browser (less, cooffee, typescript) transforma/transpila arquivos que o browser possa entender (javascript/css...). Também e muito usado para versões de javascript que seu browser não suporta.

- **Debbuger:** Permite debugar seu codigo em qualquer derivado (cooffee, typescript, javascript desatualizado e etc)

- **Servidor Dev:** Tem o seu proprio servidor de desenvolvimento, neste servidor e utilizado o Express um pacote do nodejs. Lembrando que quando esta em ambiente de desenvolvimento os arquivos de bundle nao sao gerados, ficam armazenado na memoria

**Como instalar?**
------------
1. Instale as dependencia do webpack e do seu ambiente de desenvolvimento
`npm i-g webpack webpack-dev-server`

2. Instale as depencias dentro do seu projeto como desenvolvimento
`npm i webpack webpack-dev-server -D`

------------

**Eu tenho certeza que já ficou confuso vendo aqueles códigos do webpack não é mesmo? Se não ficou pode ter certeza que um dia vai ficar kkkk, abaixo descrevo alguns exemplos de código do webpack para ir se familiarizando.**

Antes de mostrar um pouco sobre o arquivo de configuração do webpack, lembre se de sempre configurar seus 'scripts' do **package.json** para receber os codigos webpack

 Em package.json deverá ser editado o campo 'scripts' para ambiente de desenvolvimento e outro para buildar sua aplicação

```javascript
// --inline o browser sempre dará refresh ao modifcar algum codigo
// Hot => Hot Module Replacement na hora do refresh automatico ele substitui somente o modulo alterado

"scripts":{
	 // Configurando para ambiente de desenvolvimento
	"dev": "webpack-dev-server --content-base build --inline --hot",
	// Configurando para o build
	"build": "NODE_ENV=production webpack -p"
}
```
Para rodar o webpack em desenvolvimento digite **`npm run dev`** ou para buildar **`npm run build`**

Trechos de código do WEBPACK
------------

Qualquer tipo de configuração do webpack e feito em cima de um arquivo que sempre ficará na raiz do seu projeto, um arquivo chamado **webpack.config.js**

**OBS:** Os Códigos estarão comentados para explicar o que é cada coisa.

#### 1. Exemplo: Ponto de entrada e saída

```javascript
// Instanciar o webpack
const webpack = require('webpack');

// Para nao termos problemas com o sistema operacional usaremos o path do nodejs
const path = require('path');
// __dirname é uma variavel do nodejs para a raiz do projeto
const resolvePath = (pathToResolve = '') => path.resolve(__dirname, pathToResolve);

module.exports = {
	entry: resolvePath('src/js/app.js'), // Ponto de entrada
	output: { // Saída
		path: resolvePath('build'), // Pasta do bundle
		filename: 'bundle.js' // Nome do arquivo que será gerado o bundle
	},
}
```
#### 2. Exemplo: Loaders (Transpiler)

```javascript
module: {
	loaders: [{
		test: /.js[x]?$/,  // Extensão do arquivo (Regexp)
		loader: 'babel-loader', // Transpilador que cuidará desté código
		include: [resolvePath('src']), // Inclui uma pasta para o verificar o código
		exclude: /node_modules/, // Pasta que o transpilador irá ignorar
	},]
},
```

#### 2.2: Exemplo: Ler arquivos css em javascript
-	Em alguns frameworks de javascript é muito comum fazer importacao de arquivos **css** em arquivos **javascript** porem nativamente isso não é possivel, mas com o webpack é possivel fazer isso, utilizando um css-loader + style-loader, veja abaixo um exemplo.

-	Instale as dependencias de desenvolvimento do css loader e style-loader: `npm i -D css-loader style-loader`
-	Acrescente esté trecho de código no loaders

````javascript
{
	teste: /\.css$/, // Nome da extensao (Regexp)
	include: [resolvePath('src/css']], // Pasta que sera scaneado pelo loader (nao obrigatorio)
	loader: 'style!css' // Loader do css
}
````
Com webpack podemos ocultar a extensao dos nossos arquivos na hora de importar.

#### 3: Exemplo: Ocultar extensões dos arquivos
````javascript
resolve: {
	extension: ['', '.webpack.js', '.web.js', '.js', '.scss']
}
````

Pode ser adicionado plugins ao webpack na hora de gerar o bundle, exemplo para minificar os arquivos.

#### 4: Exemplo: Minificar arquivos na hora do bundle
````javascript
// Crie está variavel depois dos imports do arquivo de configuração
const isProductionEnvironment = process.env.NODE_ENV === 'production';
// Variavel process.env.NODE_ENV foi setado igual production no arquivo package.json no script de build

plugins: isProductionEnvironment ? [
	new webpack.optimize.UglifyJsPlugin({
		compress: { warnings: false }
	})
] : []
````

###### Fonte: [Webpack Tutorial](https://www.youtube.com/watch?v=dHWyO8U0zhc&index=1&list=PLhxF6V44XvXR05fSeNf38-67k3FZK2KLI "Webpack Tutorial"), [Site/Github webpack](https://webpack.js.org "Site/Github webpack")
