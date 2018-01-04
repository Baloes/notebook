# Busca Ternária (Ternary Search)

Semelhante a uma busca binária, a busca ternária também pode ser usado para achar uma posição de um valor em um vetor. Porém seu diferencial
é que enquanto a busca binária consegue achar um determinado ponto em uma função crescente ou decrescente, a busca ternária pode achar um
determinado valor em uma função unimodal, que é uma função que possui apenas um valor de máximo ou mínimo. Achar esses valores é justamente
o que a busca ternária faz. Perceber em um problema de maratona o uso da busca ternária no problema pode ser dificil e requerer um pouco de
criatividade.

## Links

https://en.wikipedia.org/wiki/Ternary_search
https://www.hackerearth.com/practice/algorithms/searching/ternary-search/tutorial/
https://github.com/Baloes/discussoes/blob/master/Discuss%C3%A3o%20Treino%2023-06-17.pdf<br>(Problema Supermercado)

## Problemas

https://www.urionlinejudge.com.br/judge/pt/problems/view/1860<br>
https://www.urionlinejudge.com.br/judge/pt/problems/view/1294

## Código

```c
/*
 * Precondições: o vetor de elementos usado na entrada deve estar ordenado de forma crescente.
 * Complexidade: O(log n)
 * Entrada: *v: vetor de elementos ordenados; l: limite esquerdo;
 *          r: limite direito, chave: valor do elemento que está sendo buscado.
 * Saída: posição do valor do elementeo que está sendo buscado; retorna -1 se não achar.
 */
int busca_ternaria(int *v, int l, int r, int chave)
{
    if(r >= l)
    {
        int meio1 = l + (r - l) / 3;
        int meio2 = r - (r - l) / 3;
        
        if(v[meio1] == chave) return meio1;
        if(v[meio2] == chave) return meio2;
        
        if(chave < v[meio1]) return busca_ternaria(l, meio1 - 1, x);
        else if(chave > v[meio2]) return busca_ternaria(meio2 + 1, r, x);
        else return busca_ternaria(meio1 + 1, meio2 - 1, x);
    }
    
    return -1;
}
```

O seguinte código mostra um exemplo de como achar o máximo de uma função usando a busca ternária.

```c
double func(double x)
{ 
    return -1 * 1 * x * x + 2 * x + 3; 
}

/*
 * Complexidade: O(log n)
 * Entrada: inicio: valor mais esquerda do intervalo da função;
 *          fim: valor mais a direito do intervalo da função;
 * Saída: valor máximo da função.
 */
double busca_ternária(double inicio, double fim)
{
    double l = inicio, r = fim;

    for(int i = 0; i < 200; i++) 
    {
        double l1 = (l * 2 + r) / 3;
        double l2 = (l + 2 * r) / 3;
        
        if(func(l1) > func(l2))
            r = l2; 
        else 
            l = l1;
    }

    double x = l;
    
    return func(x);
}
```
