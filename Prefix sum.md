# Prefix sum

É uma técnica utilizada quando queremos obter a soma do intervalo de um vetor em tempo constante (um número fixo de operações). Obtemos isso fazendo um pré-processamento do vetor: criamos um vetor auxiliar que contém a soma acumulada dos elementos do vetor original. Isso é, prefix[i] contém a soma acumulada dos elementos v[0], v[1], ..., v[i]. Depois, para obter a soma de um intervalo [i, j], pegamos a soma de todos os elementos até j (ou seja, prefix[j]) menos a soma dos elementos até i-1 (ou seja, prefix[i-1]). Isso é, percorremos uma vez o vetor inicialmente (pré-processamento); depois, com apenas uma subtração obtemos o valor do intervalo [i,j] do vetor.<br><br>
Há duas versões levemente diferentes. Em uma delas, prefix[i] guarda a soma dos elementos [0, i]; ou seja, prefix[0] = v[0]. Na outra, prefix[i] guarda a soma dos elementos [0, i-1]; ou seja, prefix[0] = 0, e prefix[1] = v[0]. Nesse segundo caso, o vetor prefix tem n+1 posições. Eu prefiro a segunda versão, pois torna a soma do intervalo mais simples; na primeira versão, quando i = 0, i-1 dará -1, que é um índice inválido, precisamos cuidar desse caso. Na segunda versão, não temos esse problema.

![Exemplo](https://s9.postimg.org/z5g02yc5b/Untitled-2.png)

## Links

https://en.wikipedia.org/wiki/Prefix_sum

## Problemas

Diversos exemplos: http://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/<br>

## Código

```c
/*
 * Entrada: *v: vetor de elementos; n: número de elementos; *prefix: vetor que será preenchido com a prefix sum.
 * Saída: vetor prefix estará preenchido.
 */

void preprocessamento(int *v, int n, int *prefix)   // prefix tem tamanho n+1
{
    int i;

    prefix[0] = 0;
    for(i = 0; i < n; i++)
        prefix[i+1] = prefix[i] + v[i];
}

/*
 * Entrada: i: início do intervalo; j: fim do intervalo
 *          O intervalo é fechado, ou seja, queremos calcular a soma dos índices [i, j] (indexados em 0)
 * Saída: soma do intervalo
 */
int soma_intervalo(int i, int j)
{
    return prefix[j+1] - prefix[i];
}
```
