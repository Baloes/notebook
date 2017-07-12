# Flood Fill

A flood fill é um algoritmo que serve para fazer uma área conectada ao um nó em um dado vetor multi-dimensional. Um critério de
conexão pode ser se dois nós compartilham a mesma cor, por exemplo.

Para exemplificar, supomos que queremos preencher a área inferior esquerdo com 'x', para isso podemos aplicar o flood fill
na coordenada (3, 0)

o o o o o o o o<br>
x x x o o o o o<br>
o o o x o o o o<br>
o o o x o o o o<br>
o o o x o o o o<br>

Após aplica, temos a seguinte configuração

o o o o o o o o<br>
x x x o o o o o<br>
x x x x o o o o<br>
x x x x o o o o<br>
x x x x o o o o<br>

## Problemas

https://www.urionlinejudge.com.br/judge/pt/problems/view/1907

## Código

O algoritmo pode ser implementado de várias formas, as seguir é apresentado uma possível implementação.

```c
int int v[300][300;

/*
 * Complexidade: O(?)
 * Entrada: *v: vetor de elementos ordenados; n: número de elementos;
 *          chave: valor do elemento que está sendo buscado.
 */
void flood_fill(int x, int y, int cor, int nova_cor, int N, int M)
{
  if(x < 0 || x >= N || y < 0 || y >= M)
    return;
    
  if(v[x][y] != cor)
    return;
    
  v[x][y] = nova_cor;
   
  flood_fill(x + 1, y, cor, nova_cor, N, M);
  flood_fill(x - 1, y, cor, nova_cor, N, M);
  flood_fill(x, y + 1, cor, nova_cor, N, M);
  flood_fill(x, y - 1, cor, nova_cor, N, M);
}

```
