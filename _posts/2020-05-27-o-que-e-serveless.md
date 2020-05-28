---
title: "O que é Serveless?"
published: true
---
Existem 2 paradigmas no serverless, BaaS e FaaS

#### BaaS
---
Banco de dados, serviços de autenticação, analytics e outros acessíveis diretamente via APIs.

Um exemplo bom de BaaS é o Firebase um banco de dados em tempo real da google. 

O Firebase disponibiliza autenticação, banco de dados, analytics entre muitas outras coisas... Caso queira fazer alguma coisa deste tipo o código do serviço fica dentro da sua aplicação, e não mais do lado do servidor, voce só faz uma chamada com poucas linhas de código ou seja, todo código fica no cliente e o servidor você não se preocupa.

A grande questão e que o desenvolvedor não precisa de se preocupar com o servidor e sim focar na aplicação.

### FaaS
----

Logica server-side disparada por eventos e que executa em contêineres stateless gerenciados por um terceiro (provedor de servico de FaaS)

Neste modelo a logica fica no lado do servidor, não ira rodar na aplicação cliente.

É um código que e disparado por algum tipo de evento e ele executa em algum contêiner stateless (sem estado) e gerenciado por terceiros, o desenvolvedor não precisa estanciar nada, não precisa perder tempo com docker ou saber configurar o servidor.

Um exemplo disso e o Google Cloud Functions você dispara um evento que chama as funções do lado do servidor (exemplo uma chamada HTTP).

----
[Fonte 1](https://www.youtube.com/watch?v=aIuCJmFVqwc&feature=youtu.be "Fonte 1")
[Fonte 2](https://canaltech.com.br/infra/o-que-e-e-para-quem-e-indicado-a-serverless-computing-119782/ "Fonte 2")
