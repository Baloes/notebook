# Algoritmo de Kruskal

O algoritmo de Kruskal é um algoritmo que encontra a árvore geradora mínima (MST - Minimum Spanning Tree) de um grafo bidirecional. Uma árvore geradora mínima é um subgrafo do grafo original que é uma árvore (não tem ciclos), conecta todos os vértices e cujo peso, dado pela soma dos pesos das arestas da árvore, é minimizado. Se o grafo não era inicialmente conexo, então o algoritmo de Kruskal encontrará a floresta geradora mínima - uma MST para cada componente conexo.

O algoritmo funciona da seguinte forma. Primeiro, armazenamos todas as arestas em um vetor, e ordenamos por ordem crescente dos pesos. Agora, processamos as arestas uma por uma, conferindo se, caso adicionarmos esta aresta à MST, ela formará um ciclo. Se isso for verdade, então não adicionamos a aresta à MST (pois a árvore não pode ter ciclos). Senão, adicionamos a aresta à MST. Para conferir de forma eficiente se a aresta formará um ciclo, usamos a estrutura Union-Find.

![Exemplo](https://upload.wikimedia.org/wikipedia/commons/thumb/8/87/Kruskal_Algorithm_6.svg/286px-Kruskal_Algorithm_6.svg.png)

## Links

https://pt.wikipedia.org/wiki/Algoritmo_de_Kruskal<br>
https://www.youtube.com/watch?v=fAuF0EuZVCk<br>
https://www.youtube.com/watch?v=6aeu01RtKTU&t=3561s<br>

## Problemas

https://www.urionlinejudge.com.br/judge/pt/problems/view/1152<br>
https://www.urionlinejudge.com.br/judge/pt/problems/view/1402<br>
https://www.urionlinejudge.com.br/judge/pt/problems/view/1552<br>
https://www.urionlinejudge.com.br/judge/pt/problems/view/1764<br>
https://www.urionlinejudge.com.br/judge/pt/problems/view/1956<br>
https://www.urionlinejudge.com.br/judge/pt/problems/view/2683<br>

## Código

``` c++

struct edge {
    int a, b, custo;	// aresta ligando vértices 'a' e 'b' com custo 'custo'
};

bool comp(edge a, edge b)
{
    return a.custo < b.custo;
}

// Union-find
int pai[MAXN];      // MAXN = maior número de nós na entrada

int findset(int x)
{
    if(x != pai[x])
        pai[x] = findset(pai[x]);
    return pai[x];
}

vector<edge> grafo, mst;    // o grafo e a MST são armazenados como um vetor de arestas
int n;                      // número de nós do grafo

/*
 * Entrada: 'grafo': vetor de arestas que compõem o grafo; 'n': número de nodos do grafo.
 * Saída: a função retorna o custo da MST; na variável 'mst' guardam-se as arestas da árvore geradora mínima.
 */
int kruskal()
{
    // inicializamos a union-find
    for(int i = 0; i < n; i++)
        pai[i] = i;

    // ordenamos arestas por ordem crescente de custo
    sort(grafo.begin(), grafo.end(), comp);

    int custo = 0;

    for(int i = 0; i < e; i++)
    {
        int pa = findset(grafo[i].a);
        int pb = findset(grafo[i].b);

        // se 'a' e 'b' não estão no mesmo conjunto (ou seja, adicionar essa aresta não formará ciclo),
        // então adicionar aresta na MST
        if(pa != pb)
        {
            custo += grafo[i].custo;
            pai[pa] = pb;
            mst.push_back(grafo[i]);
        }
    }

    // retornamos o custo da MST (em vários problemas apenas isso é pedido, e não a MST em si)
    return custo;
}
```
