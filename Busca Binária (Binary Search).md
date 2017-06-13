# Busca Binária (Binary Search)

A busca binária pertence a uma classe de algoritmos de busca. Semelhante a busca sequencial, seu objetivo é descobrir se um vetor possui ou não determinado elemento (chave), porém seu uso pode se extender a mais problemas. Para funcionar é necessário que o objeto da busca esteja ordenado.
A ideia de seu funcionamento consiste em eliminiar áreas que não são interessantes para busca, a medida que ela é realizada. Para isso, em cada iteração ela utilza três informações: o limite inferior do vetor, o limite superior e o meio relativo a esses limites. A medida que a busca é feita, o valor dessas informações são alterados da seguinte forma:
* Se o valor do vetor com índice igual ao "meio" for menor que a chave, então isso quer dizer que o elemento que está sendo procurado, se existe no vetor, está no intervalo (meio, limite superior];
* Se o valor for maior que a chave, então o elemento se existe no vetor, está no intervalo [limite inferior, meio); 
* Se o valor for igual a chave, então o algoritmo achou o que procurava.

A figura exemplica o comportamento do algoritmo:

![Exemplo](http://www.dainf.ct.utfpr.edu.br/wiki/images/2/21/Busca_Bin%C3%A1ria.jpg)

## Links

https://www.ime.usp.br/~pf/algoritmos/aulas/bubi2.html<br>
https://en.wikipedia.org/wiki/Binary_search_algorithm

## Problemas

https://www.urionlinejudge.com.br/judge/pt/problems/view/1025
https://www.urionlinejudge.com.br/judge/pt/problems/view/1549
https://www.urionlinejudge.com.br/judge/pt/problems/view/1586
https://www.urionlinejudge.com.br/judge/pt/problems/view/2329

## Código

```c
/*
 * Precondições: o vetor de elementos usado na entrada deve estar ordenado de forma crescente.
 * Complexidade: O(log n)
 * Entrada: *v: vetor de elementos ordenados; n: número de elementos;
 *          chave: valor do elemento que está sendo buscado.
 * Saída: posição do valor do elementeo que está sendo buscado; retorna -1 se não achar.
 */

int busca_binaria(int *v, int n, int chave)
{
    int inf = 0, sup = n - 1, meio = (sup + inf) / 2;

    while(inf <= sup)
    {
        if(v[meio] == chave)
        {
            return meio;
        }
        else if(v[meio] > chave)
        {
            sup = meio - 1;
        }
        else
        {
            inf = meio + 1;
        }

        meio = (sup + inf) / 2;
    }
    
    return -1;
}
```

Existe um algoritmo que usa uma ideia muito semelhante a busca binária, porém invés de trabalhar com vetores (discreto) trabalha com uma função real (contínua) que é sempre crescente ou descrescente no intervalo de interesse da busca. 

```c
#define LIMIT 100

/*
 * Entrada: x: valor de do x da função. 
 * Saída: valor da função naquele ponto.
 */
double funcao_real(double x)
{
    return 4 * x + 3; // função linear (ax+b)
}

/*
 * Precondições: a função real utilizada deve continua e ser sempre crescente ou decrescente.
 * Complexidade: O(log n)
 * Entrada: a: limite inferior; b: limite superior; chave: valor que está sendo buscado;
 * Saída: valor de x em que função retorna a chave.
 */
double bisseccao(double a, double b, double chave)
{
    double inf = a, sup = b, meio = (sup + inf) / 2;
    int it = 0;
    
    while(it++ < LIMIT)
    {
        double y = funcao_real(meio);
        
        if(y == chave)
        {
            return meio;
        }
        else if(y > chave)
        {
            sup = meio;
        }
        else
        {
            inf = meio;
        }

        meio = (sup + inf) / 2;
    }
    
    return meio;
}
```

Obs: O valor limite número de iterações máximas que serão realizadas (LIMIT == 100 muitas vezes pode ser suficiente para retornar o resultado correto). Devido a possíveis problemas de precisão, mesmo que a chave exista na função, o computador pode interpretar como dois números diferentes.
