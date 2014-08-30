---
layout: post
title:  "Entenda Ponteiros em C de uma vez por todas!"
date:   2014-08-27 12:21:00
author: "Vinícius do Carmo"
author_contact: "http://vinimdocarmo.github.io"
tags: C, ponteiros, programação, CK0110
---

Uma das coisas que os iniciantes em C sentem mais dificuldade é o conceito de ponteiros. O propósito desse post é fornecer uma introdução para ponteiros e seus usos para estes iniciantes.<!--more-->

Na maioria dos casos, um dos motivos que levam ao não entendimento de ponteiros é que os iniciantes na linguagem têm uma fraqueza ou pouco entendimento sobre variáveis(como elas são usadas em C). Então iremos dar uma pequena explicação geral de variáveis.

### Variáveis em C

Uma variável em um programa é algo com um **nome** e um **valor** (que pode variar). A maneira que o [compilador](http://pt.wikipedia.org/wiki/Compilador) lida com esse **nome** e esse **valor** é tal que ele aloca um específico bloco de memória dentro do computador para guardar o **valor** daquela variável. O tamanho desse bloco de memória vai depender do tipo da variável. Por exemplo, em um computador de 32 bits, o tamanho de uma variável do tipo `int` é 4 bytes.

Se você quer saber os tamanhos dos tipos de variáveis em C no seu sistema operacional, rode o seguinte trecho de código especificando o tipo. `int`, por exemplo:

{% highlight c %}
#include <stdio.h>
#include <stdlib.h>

int main(/*...*/) {
  printf("Tamanho de uma variável do tipo int %d\n", sizeof(int));

  return EXIT_SUCCESS;
}
{% endhighlight %}

Quando declaramos uma variável, nós temos que informar ao compilador duas coisas: o nome da variável e o tipo dela. Por exemplo, nós declaramos uma variável do tipo **int** com o nome **k** escrevendo:

{% highlight c %}
int k;
{% endhighlight %}

Ao ver "int" nesse trecho de código, o compilador aloca 4 bytes em um lugar específico da memória para setar o valor inteiro. Ele também cria uma [tabela de símbolos](http://pt.wikipedia.org/wiki/Tabela_de_s%C3%ADmbolos). Nessa tabela ele adiciona o símbolo **k** mapeando o seu endereço relativo da memória onde aqueles 4 bytes estão alocados.

Se escrevermos depois...

{% highlight c %}
k = 2;
{% endhighlight %}

...nós esperamos que em tempo de execução, quando esse trecho de código for executado, que o valor 2 seja colocado naquele espaço de memória que foi alocado anteriormente para guardar o valor de **k**. Em C, nos referiamos a uma variável, como o inteiro **k**, como um "objeto".

Com isso, podemos dizer que existem dois "valores" associados com o objeto **k**. Um é o valor do inteiro guardado nele (2, no exemplo acima) e o outro o "valor" da localização da memória, isto é, o endereço de **k**. Algumas bibliografias referenciam esses dois valores com a nomenclatura __*rvalue*__ (*right value*, pronunciado "*are value*") e __*lvalue*__ (*left value*, pronunciado "el value"), respectivamente.

Ok, agora considere:

{% highlight c linenos %}
int j,k;

k = 2;
j = 7; 
k = j; 
{% endhighlight %}

No exemplo acima, o compilador interpreta o **j** na linha 4 como sendo o endereço da variável **j** (seu __*lvalue*__) e copia o valor 7 para aquele endereço. Entretando, na linha 5 o **j** é interpretado como seu __*rvalue*__ (desde que esteja no lado direito do operador de atribuição `=`). Ou seja, aqui o **j** refere-se ao valor armazenado no local de memória alocado para **j**, nesse caso 7. Então o 7 é copiado para o endereço de memória designado para o __*lvalue*__ de **k**.

### Ponteiros em C

Agora, digamos que nós temos uma razão para querer que uma variável seja designada a guardar um __*lvalue*__ (um endereço). Tal variável é chamada de **variável ponteiro** (por razões que irão se tornar mais claras depois). Em C, quando queremos definir uma variável ponteiro, colocamos um arterísco antes do nome da variável. Em C, nós também damos a nossa variável ponteiro um tipo que, nesse caso, refere-se ao tipo de dado guardado no endereço que iremos guardar na nossa variável ponteiro. Por exemplo, considere a declaração de variável ponteiro:

{% highlight c %}
int *ptr;
{% endhighlight %}

**ptr** é o nome da nossa variável (tal como **k** foi o nome da nossa variável no exemplo mais acima). O `*` informa ao compilador que nós queremos uma variável ponteiro, isto é, alocar uma quantidade de bytes necessária para guardar um endereço na memória. O `int` diz que nós pretendemos usar nosso ponteiro para guardar um endereço de um inteiro. Tal variável "aponta" para um inteiro. Entretanto, note que quando escrevemos `int k;` nós não demos a `k` um valor. Se essa declaração for feita fora de qualquer função, a variável `k` será inicializada com o valor 0. Similarmente, não atribuímos nenhum valor a `ptr` na declaração do exemplo acima. Nesse caso, se a declaração também for feita fora de qualquer função, `ptr` será inicializado com um certo valor que garante não "apontar" para nenhum objeto C ou função. Uma ponteiro inicializado dessa maneira é chamado de ponteiro nulo.

Em C, um macro é usado para representar um ponteiro nulo. Esse macro vem com o nome NULL. Logo, declarar uma variável usando o macro NULL, tal como numa declaração do tipo `ptr = NULL`, garante que o ponteiro é um ponteiro nulo. 

Da mesma forma que podemos testar se um valor de uma variável inteira é igual a 0 usando`if(k == 0)`, nós também podemos testar se um ponteiro é um ponteiro nulo usando `if(ptr == NULL)`.

Suponha que agora nós queremos guardar em `ptr` o endereço da nossa variável inteira `k`. Para fazer isso nós usamos o operador unário **&** e escrevemos:

{% highlight c %}
ptr = &k;
{% endhighlight %}

O que o operador `&` faz é recuperar o __*lvalue*__ (endereço) de `k` (embora `k` esteja do lado direito do operador de atribuição `=`), e então este endereço é copiado no conteúdo do nosso ponteiro `ptr`. Agora, `ptr` está "apontando" para `k`. Agora, só tem mais um operador que precisamos discutir.

O operador unário `*` é usado da seguinte forma. Considere esse trecho de código:

{% highlight c %}
*ptr = 7;
{% endhighlight %}

O valor 7 será copiado para o endereço de memória "apontado" por `ptr`. Logo, se `ptr` "aponta para" (contém o endereço de) `k`, o que o trecho de código acima faz é atribuir 7 como sendo o valor de `k`. Ou seja, quando usamos o operador `*` dessa maneira, nós estamos nos referindo ao valor da variável para a qual `ptr` está apontando, e não para o próprio valor de `ptr`.

Dessa maneira, poderíamos escrever:

{% highlight c %}
printf("%d\n", *ptr);
{% endhighlight %}

para imprimir na tela o valor inteiro guardado no endereço que é "apontado" por `ptr`.

### Testando

Uma maneira de ver como toda essa coisa funciona seria rodar o seguinte programa e depois revisar o código e o _output_ cuidadosamente.

{% highlight c %}
#include <stdio.h>
#include <stdlib.h>

int j, k;
int *ptr;

int main(/*...*/) {
    j = 1;
    k = 2;
    ptr = &k;
    printf("\n");
    printf("j tem o valor %d e está armazenado no endereço %p\n", j, &j);
    printf("k tem o valor %d e está armazenado no endereço %p\n", k, &k);
    printf("ptr tem o valor %p e está armazenado no endereço %p\n", ptr, &ptr);
    printf("O valor do inteiro apontado por ptr é %d\n", *ptr);
    printf("\n");

    return EXIT_SUCCESS;
}
{% endhighlight %}

### TL;DR

* Uma variável é declarada dando a ela um tipo e um nome (`int k;` por exemplo)
* Uma variável ponteiro é declarada dando a ela um tipo e um nome (`int *ptr` por exemplo), onde o asterisco diz ao compilador que a variável nomeada de **ptr** será uma variável ponteiro e o tipo dela diz ao compilador para que tipo o ponteiro **ptr** irá apontar.
* Uma vez que uma variável é declarada, nós podemos pegar seu endereço colocando o operador unário **&** antes do nome da váriavel (`&k` por exemplo).
* Nós também podemos pegar o valor que está no endereço para o qual uma variável ponteiro está apontado usando o operador unário __*__ (`*ptr` por exemplo).
* Um __*lvalue*__ de uma variável é o "valor" do endereço de onde esta variável está armazenada. O __*rvalue*__ de uma variável é o valor que está armazenado nessa variável (naquele endereço).