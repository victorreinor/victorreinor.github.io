---
title: "O que é React?"
published: true
---
# O que é React?
**Biblioteca** para construções de **interfaces**;
Tudo que o usuário enxergar **Layout** (html, css, javascript).

Utilizado para construção **SPA** (Single-Page-Applications), um conceito que veio junto com **Angular** no começo de 2011, este conceito é uma forma de você construir aplicações no front-end. Antes do conceito **SPA** nos tinhamos o back-end e para cada rota ele retornava todo o conteudo html montado, um exemplo é o **PHP** aonde era digitado todo código html, as querys do banco de dados e javascript (Ficava uma mistureira só 🤢🤢). Hoje em dia ficou mais fácil, fazemos aplicações separadas que chamamos de **front-end** e **back-end**, no front-end consumimos o back-end por via **URL'S HTTP** e montamos todo nosso layout com base em dados **JSON**.

React é um **framework**?
Sim, só o **React** e uma **LIB** (Biblioteca) mas quando analisamos o ecossistema inteiro do React podemos chamar de Framework pois tudo que vem crescendo em volta do React fez com que muitas coisas fosse usadas em conjuntos não somente uma simples LIB de interfaces, um exemplo e o **JSX**.

React/ReactJs/React-Native

**React**: É a biblioteca de construção de interfaces e componentização que é utilizada tanto no **REACTJS** quanto no **REACT-NATIVE**.

**ReactJS**: ReactJS diretamente no browser, usamos a biblioteca **react-dom** para manipulação da arvore de elementos do **browser**

**React-Native**: Para desenvolvimentos de aplicativos nativos **android** e **ios**, que usa biblioteca que lida com elementos nativos de cada plataforma.

O melhor de tudo é que tudo é **JAVASCRIPT** 🚀🚀.

## Vantagens
- **Componentização**
  - Consiste em dividir parte do nosso código em componentes que tem funcionalidades especificas (Vejamos a imagem abaixo);
  - Vemos o **CommentForm** ele basicamente um formulário para adicionar comentarios, qualquer tela que quisermos chamar este formulário é so instanciar o componente e colocar na tela e assim por diante;
[![React Component Tree](https://raw.githubusercontent.com/victorreinor/o-que-e-react/master/react-component-tree.webp "React Component Tree")](https://raw.githubusercontent.com/victorreinor/o-que-e-react/master/react-component-tree.webp "React Component Tree")
  - **Quando componentizar?** Componentização acontece quando conseguimos isolar a logica do componente de forma que não afetara o restante da aplicação.
- **Divisão de responsabilidades**
  - Deixamos o front-end somente para interfaces e nosso back-end cuidando da nossa regra de negocio, por exemplo um carrinho de compras quando adicionamos um cupom de desconto, calculamos os descontos no nosso back-end para nao ter nenhuma interferencia do front-end
- **API e Vários clientes**
  - Criamos somente uma api e podemos criar diversas aplicações para consumir a mesma pois temos um servidor servindo os dados.
