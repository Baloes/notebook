# Grafos

Grafos é tópico bastante comum na maratona de programação. Entender o que eles são é fundamental para ter um bom desempenho
na competição. Nesse tópico é introduzido alguns conceitos sobre grafos em conjunto com alguns algoritmos básicos.

notação de um grafo: G(V, E); V representa um conjunto de arestas e E representa um conjunto de arestas. Uma aresta é uma
tupla (u, v), em que representa uma ligação entre dois vértices, u e v.

## Conceitos

**Vértice:** Um grafo é composto de vértices (ou nodos, pontos, estados). Ele pode representar qualquer informação.

**Arestas**: Vértices são conectados por arestas (ou arco, linha). Uma aresta representa uma relação entre vérices.

**Grafo direcionado:** Um grafo direcionado é que a direção da conexão entre dois vértice importa (i.e. uma rua de mão única
que liga dois pontos, ou seja, se A tem conexão com B, então não quer dizer que B tem uma ligação com A).

**Grafo bidericional:** Um grafo em que as arestas não tem direção, ou seja, se uma aresta liga A e B, então ela liga
B e A.

**Grafo ponderado:** Um grafo em que cada aresta pode ter um peso (ou custo i.e. distância entre duas cidades) diferente.

**Grau de entrada:** É o número de arestas que entram em um vértice.

**Grau de saída:**: É o número de arestas que saiem de uma aresta.

**Grafo fortemente conexo:** É um grafo em que todas os vértices conseguem visitar todos os outros.

**Grafo completo:** É um grafo em que todos os vértices tem relação com todos os outros.

**Grafo Cíclico:** É um grafo em que existe um vértice que possui um caminho que volta para ele. Um caminho em um grafo
é um conjunto de arestas que liga dois pontos. Um grafo que não possui ciclos é um grafo acíclico.

## Representação de grafos

Existem algumas formas de representar grafos, duas delas são mais frequentementes utilizadas na maratona. A primeira é
conhecida como **matriz adjascência** e a segunda é chamada de **lista encadeada**. A escolha de qual estrutura utilizar
depende muito do problema que está tentando resolver. Mais detalhes serão explicado futuramente, ou em caso de dúvidas
procure algum maratonista mais experiente.

### Matriz adjascência

Para representar um grafo utilizando matriz adjascência utiliza um vetor bidimensional. Cada índice de uma linha da matriz representa
um vértice o índice da coluna representa um outro vértice. Por exemplo, caso a posição da matriz [0][5] esteja igual a um valor
igual à um, então isso quer dizer que existe uma aresta ligando o vértice 0 e 5. Note que o valor um é apenas uma convenção,
caso o grafo seja ponderado, esse valor poderia ser um valor maior que zero, em que um valor negativo poderia indicar a ausênncia
de uma relação entre dois vértices.

```c
    TODO: Inserir um exemplo de implementação usando matriz adjascência.
```

### Lista encadeada

```c
    TODO: Inserir um exemplo de implementnaço usando lista encadeada e explição sobre.
```

## Algoritmos básicos de grafos

Como introdução dois algoritmos serão apresentados para entender melhor como manipular e utilizara as estruturas para 
representar um grafo. Ambos são base de vários outros algoritmos, eles são conhecidos como **Busca em Largura (BFS)** e 
**Busca em Profundidade (DFS)**. É altamente recomendado que implemente esses algoritmos utilizando o c++, pois as estruturas
auxiliares para implementar eles já está disponível na linguagem, ao contrário da linguagem c. Para melhor entendimento dos
algortimos apresentados abaixo, busque mais informações em outros meios. Digite no google e leia sobre.

### Busca em Largura (BFS)

Código utilizando matriz adjascência:

```cpp
int grafo[10][10] = {}; // tamanho da matriz dependend do problema i.e. maior numero de vertices possivel

void bfs(int origem)
{
   queue<int> proximo;
   int visitado[10] = {}; // para evitar visitar um mesmo vertice mais de uma vez
   
   proximo.push(origem);
   visitado[origem]
   
   while(!proximo.empty()) // enquanto restar alguem para ser visitado
   {
      int u = proximo.front(); // tira o proximo vertice a ser visitado
      proximo.pop(); // remove o vertice da fila
      
      for(int v = 0; v < 10; v++)
      {        
        if(grafo[u][v] && !visitado[v]) // se existe uma aresta entre u e v e se v ainda nao foi visitado
        {
          proximom.push(v); // insere v na fila
          visitado[v] = 1; // marca como visitado
        }
      }
   }
}
```

Código utilizando lista encadeada:

```c
    TODO: Adicionar após adicionar explicação de lista encadeada
```

## Busca em Profundidade (DFS)

Código utilizando matriz adjascência:

```c
int matriz[10][10] = {};
int visitado[10] = {};

void dfs(int u)
{
  visitado[u] = 1;
  
  for(int v = 0; v < 10; v++)
  {
    if(grafo[u][v] && !visitado[v])
    {
      dfs(v);
    }
  }
}
```

**Obs:** Note que ambas as implementação faz nada além de visitar todos os vértices. Um problema poderia saber se existe um 
caminho entre dois vértices, u e v, para isso poderia aplicar uma BFs a partir de u e se visitado[v] no final da 
busca estiver igual 1, então existe um caminho entre u e v. Outro problema poderia ver se o grafo é conexo, então
poderia a partir de qualquer vertice aplicar uma BFS e se todos no final da busca forem visitado, então o grafo
é conexo. Para isso poderia checar se todo o vetor de visitado está com valor um, ou adicionar uma variável
contadora que incrementa sempre que um vertice novo é visitado, então depois checa se o contador tem um valor
igual ao número de vertices do grafo.
