# Sublista contígua de soma máxima

Dada uma lista de números, queremos encontrar o intervalo contíguo de soma máxima. Se utilizarmos Prefix Sum (descrito no notebook), podemos resolver com complexidade quadrática (aproximadamente n^2 operações: testamos todos os pontos de início de intervalo e todos os pontos de fim, e utilizamos Prefix Sum para obter a soma de cada intervalo em tempo constante). O algoritmo ótimo, por vezes chamado Algoritmo de Kadane, tem complexidade linear (faz aproximadamente n operações).<br>
Nos códigos abaixo, se todos os números da lista forem negativos, o algoritmo retorna 0 (ou seja, a sublista de maior soma seria a lista vazia). Nesse caso, a sublista de maior soma tirando a lista vazia seria uma lista com apenas o maior elemento da lista. Se esse caso for posível, é necessário o que o problema quer que seja feito.

![Exemplo](http://www.geeksforgeeks.org/wp-content/uploads/kadane-Algorithm.png)

## Links

https://pt.wikipedia.org/wiki/Sublista_cont%C3%ADgua_de_soma_m%C3%A1xima<br>
http://www.geeksforgeeks.org/largest-sum-contiguous-subarray/<br>

## Problemas

https://www.urionlinejudge.com.br/judge/pt/problems/view/2191<br>
https://www.urionlinejudge.com.br/judge/pt/problems/view/2463<br>
http://br.spoj.com/problems/BAPOSTAS/<br>

## Código

```c
/*
 * Entrada: *v: vetor de elementos; n: número de elementos.
 * Saída: soma da sublista contígua de soma máxima.
 */

#define max(a,b) (a > b ? a : b)

int maior_soma_contigua(int *v, int n)
{
    int maior = 0, atual = 0, i;

    for(i = 0; i < n; i++)
    {
        atual += v[i];

        atual = max(atual, 0);
        maior = max(maior, atual);
    }

    return maior;
}

/*
 * Entrada: *v: vetor de elementos; n: número de elementos.
 * Saída: maior: soma da sublista contígua de soma máxima.
          [ini, fim]: intervalo da soma máxima.
 */
void intervalo_maior_soma_contigua(int *v, int n)
{
    int maior = 0, atual = 0, i, ini_atual = 0, ini = -1, fim = -1;

    for(i = 0; i < n; i++)
    {
        atual += v[i];

        if(atual < 0)
        {
            atual = 0;
            ini_atual = i+1;
        }
        if(atual > maior)
        {
            maior = atual;
            ini = ini_atual;
            fim = i;
        }
    }
}
```
