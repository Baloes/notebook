# Máximo Divisor Comum (MDC) e Mínimo Múltiplo Comum. 

O maior divisor comum (mdc) de dois números a, b é o maior inteiro positivo d, tal que d | a e d | b. Um uso do mdc é simplificar uma fração, dividindo tanto o numerador e o denominador pelo seu mdc. Apesar de existir problemas que cobram apenas o uso do mdc, em competições como a Maratona de Programação seu uso é mais provável como parte de uma solução maior.

```c
int mdc(int a, int b) 
{
    return b == 0 ? a : mdc(b, a % b);
}
```

O mdc está relacionado com o mínimo múltiplo comum (mmc) da seguinte forma: mdc(a, b) * mmc(a, b) = a * b. Com isso é possível usar o mdc para descobrir o mmc. 

```c
int mmc(int a, int b)
{
    return a * (b / mmc(a, b));
}
```
## Links

https://en.wikipedia.org/wiki/Greatest_common_divisor

## Problemas

### MDC
https://www.urionlinejudge.com.br/judge/pt/problems/view/1028<br>
https://www.urionlinejudge.com.br/judge/pt/problems/view/1307<br>
https://www.urionlinejudge.com.br/judge/pt/problems/view/2204<br>
https://www.urionlinejudge.com.br/judge/pt/problems/view/2494<br>

### MMC
https://www.urionlinejudge.com.br/judge/pt/problems/view/1909<br>
https://www.urionlinejudge.com.br/judge/pt/problems/view/2514
