# Problema da soma dos subconjuntos (Subset Sum)

Dada uma lista de números, queremos saber se há algum subconjunto cuja soma seja igual a X. Usamos um vetor para marcar quais valores de soma já foram encontrandos: possivel[j] é verdadeiro se encontramos um subconjunto cuja soma seja j. Inicialmente, apenas possivel[0] é verdadeiro. Após, processamos os elementos um a um, na i-ésima iteração (processando o i-ésimo elemento), se possivel[j] é verdadeiro (significando que, com os primeiros i-1 elementos, encontramos um subconjunto de soma j) então adicionamos o i-ésimo elemento a este subconjunto e, portanto, possivel[j + v[i]] é verdadeiro também. A complexidade do algoritmo é O(n * X), ou seja, o número de operações é proporcional ao número de elementos vezes a soma desejada.<br><br>
É preciso tomar cuidado no caso em que houver elementos negativos, ou que a soma desejada seja negativa, pois pode haver acessos inválidos no vetor (tentar acessar índices abaixo de 0 ou acima do limite). Os códigos abaixo são feitos considerado que todos os elementos são não negativos.

![Exemplo](https://s18.postimg.org/bjo8xp0vt/image.png)

## Links

https://pt.wikipedia.org/wiki/Problema_da_soma_dos_subconjuntos<br>

## Problemas

https://www.urionlinejudge.com.br/judge/pt/problems/view/2228<br>
https://www.urionlinejudge.com.br/judge/pt/problems/view/2446<br>
http://marathoncode.blogspot.com.br/2013/01/soma-de-subconjunto-subset-sum.html<br>
http://practice.geeksforgeeks.org/problems/subset-sum-problem/0<br>

## Código

```c
/*
 * Entrada: *v: vetor de elementos; n: número de elementos; x: valor desejado da soma.
 * Saída: 1 se for possível alcançar a soma; 0 caso contrário.
 */

int subset_sum(int *v, int n, int x)
{
    int possivel[x+1] = {};
    int i, j;

    // marca que é possível alcançar a soma 0 (conjunto vazio)
    possivel[0] = 1;

    for(i = 0; i < n; i++)
    {
        for(j = x; j >= v[i]; j--)
        {
            // se for possível alcançar a soma (j - v[i]), então adicionamos o elemento 'i' nesta soma,
            // logo alcançado a soma (j)
            if(possivel[j - v[i]])
                possivel[j] = 1;
        }
    }

    return possivel[x];
}
```
