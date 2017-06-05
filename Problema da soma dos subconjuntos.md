# Problema da soma dos subconjuntos (Subset Sum)

Dada uma lista de n�meros, queremos saber se h� algum subconjunto cuja soma seja igual a X. Usamos um vetor para marcar quais valores de soma j� foram encontrandos: possivel[j] � verdadeiro se encontramos um subconjunto cuja soma seja j. Inicialmente, apenas possivel[0] � verdadeiro. Ap�s, processamos os elementos um a um, na i-�sima itera��o (processando o i-�simo elemento), se possivel[j] � verdadeiro (significando que, com os primeiros i-1 elementos, encontramos um subconjunto de soma j) ent�o adicionamos o i-�simo elemento a este subconjunto e, portanto, possivel[j + v[i]] � verdadeiro tamb�m. A complexidade do algoritmo � O(n * X), ou seja, o n�mero de opera��es � proporcional ao n�mero de elementos vezes a soma desejada.<br><br>
� preciso tomar cuidado no caso em que houver elementos negativos, ou que a soma desejada seja negativa, pois pode haver acessos inv�lidos no vetor (tentar acessar �ndices abaixo de 0 ou acima do limite). Os c�digos abaixo s�o feitos considerado que todos os elementos s�o n�o negativos.

![Exemplo](https://s18.postimg.org/bjo8xp0vt/image.png)

## Links

https://pt.wikipedia.org/wiki/Problema_da_soma_dos_subconjuntos<br>

## Problemas

https://www.urionlinejudge.com.br/judge/pt/problems/view/2228<br>
https://www.urionlinejudge.com.br/judge/pt/problems/view/2446<br>
http://marathoncode.blogspot.com.br/2013/01/soma-de-subconjunto-subset-sum.html<br>
http://practice.geeksforgeeks.org/problems/subset-sum-problem/0<br>

## C�digo

```c
/*
 * Entrada: *v: vetor de elementos; n: n�mero de elementos; x: valor desejado da soma.
 * Sa�da: 1 se for poss�vel alcan�ar a soma; 0 caso contr�rio.
 */

int subset_sum(int *v, int n, int x)
{
    int possivel[x+1] = {};
    int i, j;

    // marca que � poss�vel alcan�ar a soma 0 (conjunto vazio)
    possivel[0] = 1;

    for(i = 0; i < n; i++)
    {
        for(j = x; j >= v[i]; j--)
        {
            // se for poss�vel alcan�ar a soma (j - v[i]), ent�o adicionamos o elemento 'i' nesta soma,
            // logo alcan�ado a soma (j)
            if(possivel[j - v[i]])
                possivel[j] = 1;
        }
    }

    return possivel[x];
}
```
