# Crivo de Eratóstenes

É uma técnica utilizada para encontrar números primos até um certo valor limite. Basicamente, temos um vetor que indica se o número i é primo (se eh_primo[i] for verdadeiro, i é primo). Inicialmente, todos os números começam como primos (exceto 0 e 1). Após, iteramos de 2 até o limite desejado e, se o número da iteração atual for primo, marcamos todos os seus múltiplos como não-primos. Podemos otimizar o algoritmo, começando a marcar os múltiplos do primo i em i^2 (o porquê disso funcionar fica como exercício para o leitor, ou exercício para o leitor que sabe usar o Google).

![Exemplo](https://upload.wikimedia.org/wikipedia/commons/8/8c/New_Animation_Sieve_of_Eratosthenes.gif)

## Links

https://pt.wikipedia.org/wiki/Crivo_de_Erat%C3%B3stenes
http://www.geeksforgeeks.org/sieve-of-eratosthenes/

## Problemas

https://www.urionlinejudge.com.br/judge/pt/problems/view/2180<br>
https://www.urionlinejudge.com.br/judge/pt/problems/view/1926<br>
https://www.urionlinejudge.com.br/judge/pt/problems/view/1697<br>

## Código

```c
/*
 * Entrada: n: limite para o qual queremos encontrar os primos; *eh_primo: vetor que será preenchido.
 * Saída: vetor eh_primo estará preenchido: eh_primo[i] verdadeiro indica que i é primo.
 */

void crivo(int n, int *eh_primo)
{
    int i, j;

    // marcamos todos como primos
    for(i = 0; i < n; i++) eh_primo[i] = 1;

    // marcamos que 0 e 1 não são primos
    eh_primo[0] = eh_primo[1] = 0;

    // para otimizar levemente, primeiro marcamos que todos os pares maiores que 2 não são primos; assim, o laço seguinte
    // pode percorrer apenas os números ímpares
    for(i = 4; i < n; i += 2) eh_primo[i] = 0;
    for(i = 3; i*i < n; i += 2)
    {
        if(eh_primo[i])
        {
            // se i for primo, marcamos todos os múltiplos de i a partir de i*i como não primos
            for(j = i*i; j < n; j += i)
                eh_primo[j] = 0;
        }
    }
}

```
