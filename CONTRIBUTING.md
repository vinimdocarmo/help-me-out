[markdown]: http://daringfireball.net/projects/markdown/syntax

##Seja um autor

Dois métodos poderão ser usados para você postar sua contribuição no blog.

###Método 1 (mais complicado)

**Para usar esse método você terá que ter conhecimento em Git e Github. Caso você não tenha conhecimento nessas ferramentas, use o [método 2](https://github.com/vinimdocarmo/help-me-out/blob/master/CONTRIBUTING.md#m%C3%A9todo-2).**

Para usar esse método, você terá primeiro que seguir o [passo-a-passo](https://github.com/vinimdocarmo/help-me-out#passo-a-passo) de como colocar a aplicação para rodar em sua máquina.

Depois de ter feito o passo acima com sucesso [abra uma issue](https://help.github.com/articles/creating-an-issue) com uma descrição pequena do que você pretende falar para poder ter uma discussão a cerca do tema para saber se ele é viável. Caso seja viável, [crie um branch](https://help.github.com/articles/creating-and-deleting-branches-within-your-repository#creating-a-branch) e trabalhe nele.

Dentro do seu branch crie um arquivo na pasta `_posts` com a seguinte convensão:

```
ANO-MES-DIA-titulo-do-post.markdown
```

Onde `ANO` é representado por quatro dígitos e `MES` e `DIA` representado por dois dígitos. Por exemplo, os seguintes arquivos são nome de arquivos de postagens válidos:

```
2014-07-31-colaboracao-academica-essa-e-a-ideia.markdown
1900-05-03-postagem-antiga.markdown
```

Depois de ter criado o arquivo, a primeira coisa que você tem que fazer é configurar as variáveis de sua postagem colocando o seguinte trecho de código no começo de seu arquivo:

```
---
layout: post
title:  "O título de sua postagem"
date:   1900-01-01 11:17:00
author: "Seu nome"
author_contact: "http://url.do.seu.contato.com"
tags: minhatag1, minhatag2, minhatag3
---
```

Modifique os valores das variáveis com as informações de sua postagem. A única variável que não é obrigatória é a `tags`, mas aconcelho a colocá-las, pois será usadas em funcionalidades futuras do blog. O conteúdo de seu post deverá ser escrito abaixo dessa configuração de variáveis.

Prontinho, agora você pode colocar a mão na massa e começar a escrever sua postagem! Para uma melhor visualização e estruturação de suas postagens, utilize formatações [markdown][markdown].

Para acompanhar o andamento de seu post a medida que você vai modificando e salvando ele, execute o seguinte comando:

```
jekyll serve --watch
```
 
 Depois abra _localhost:4000_ no seu browser favorito.
 
 Terminou de escrever? Agora faça o commit de suas alterações. Porém, a issue que foi aberta no começo desse método deverá ser fechada [via commit](https://help.github.com/articles/closing-issues-via-commit-messages). Agora coloque suas alterações no projeto [via push](https://help.github.com/articles/pushing-to-a-remote) e [crie um pull request](https://help.github.com/articles/creating-a-pull-request) para aprovação. Após aprovado, sua postagem vai estar disponível no [Help Me Out](https://help.github.com/articles/creating-a-pull-request). :tada:
 
###Método 2
 
Caso você não não conheça as ferramentas requiridas pelo [método 1](https://github.com/vinimdocarmo/help-me-out/blob/master/CONTRIBUTING.md#m%C3%A9todo-1-mais-complicado), mande email para <a href="mali:helpmeout.comp@gmail.com">helpmeout.comp@gmail.com</a> com sua proposta de postagem. Iremos discutir a respeito para saber se ela é viável. Caso seja, escreva seu post usando formatação [markdown][markdown] e me mande o que você fez pela mesma thread do e-mail com a discussão a respeito da postagem.
