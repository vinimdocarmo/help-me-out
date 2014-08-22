---
layout: post
title:  "Entenda Ponteiros em C de uma vez por todas!"
date:   2014-08-22 18:30:00
author: "Vinícius do Carmo"
author_contact: "http://vinimdocarmo.github.io"
tags: 
---

Uma das coisas que os iniciantes em C sentem mais dificuldade é o conceito de ponteiros. O propósito desse post é fornecer uma introdução para ponteiros e seus usos para estes iniciantes.<!--more-->

Na maioria dos casos, um dos motivos que levam ao não entendimento de ponteiros é que os iniciantes na linguagem têm uma fraqueza ou pouco entendimento sobre variáveis(como elas são usadas em C). Então, iremos dar uma pequena explicação geral de variáveis.

### Variáveis em C

Uma variável em um programa é algo com um **nome** e um **valor**(que pode variar). A maneira que o [compilador](http://pt.wikipedia.org/wiki/Compilador) e o [lincador](http://en.wikipedia.org/wiki/GNU_linker) lhe dão com esse **nome** e esse **valor** é tal que eles atribuem um específico bloco de memória dentro do computador para guardar o **valor** dequela variável. O tamanho desse bloco de memória vai depender do tipo da variável. Por exemplo, em um computador de 32 bits o tamanho de uma variável do tipo `int` é 4 bytes.

Se você quer saber os variados tamanhos de variáveis em C no seu sistema operacional, rode o seguinte trecho de código que ele lhe dará essa informação.

{% highlight c %}
#include <stdio.h>
#include <stdlib.h>

int main(/*...*/) {
  printf("Tamanho de uma variável do tipo int %d\n", sizeof(int));
  printf("Tamanho de uma variável do tipo char %d\n", sizeof(char));

  return EXIT_SUCCESS;
}
{% endhighlight %}

Quando declaramos uma variável nós temos que informar ao compilador duas coisas, o nome da variável e o tipo dela. Por exemplo, nós declaramos uma variável do tipo `int` com o nome **k** escrevendo:

{% highlight c %}
int k;
{% endhighlight %}

Em ver "int" nesse trecho de código, o compilador aloca 4 bytes em um lugar específico da memória para setar o valor inteiro. Ele também cria uma [tabela de símbolos](http://pt.wikipedia.org/wiki/Tabela_de_s%C3%ADmbolos). Nessa tabela ele adiciona o símbolo **k** e o seu endereço relativo da memória onde aqueles 4 bytes estão alocados.

