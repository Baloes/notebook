# Algoritmo de Kruskal

O algoritmo de Kruskal � um algoritmo que encontra a �rvore geradora m�nima (MST - Minimum Spanning Tree) de um grafo bidirecional. Uma �rvore geradora m�nima � um subgrafo do grafo original que � uma �rvore (n�o tem ciclos), conecta todos os v�rtices e cujo peso, dado pela soma dos pesos das arestas da �rvore, � minimizado. Se o grafo n�o era inicialmente conexo, ent�o o algoritmo de Kruskal encontrar� a floresta geradora m�nima - uma MST para cada componente conexo.

O algoritmo funciona da seguinte forma. Primeiro, armazenamos todas as arestas em um vetor, e ordenamos por ordem crescente dos pesos. Agora, processamos as arestas uma por uma, conferindo se, caso adicionarmos esta aresta � MST, ela formar� um ciclo. Se isso for verdade, ent�o n�o adicionamos a aresta � MST (pois a �rvore n�o pode ter ciclos). Sen�o, adicionamos a aresta � MST. Para conferir de forma eficiente se a aresta formar� um ciclo, usamos a estrutura Union-Find.

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

## C�digo

``` c++

struct edge {
    int a, b, custo;	// aresta ligando v�rtices 'a' e 'b' com custo 'custo'
};

bool comp(edge a, edge b)
{
    return a.custo < b.custo;
}

// Union-find
int pai[MAXN];      // MAXN = maior n�mero de n�s na entrada

int findset(int x)
{
    if(x != pai[x])
        pai[x] = findset(pai[x]);
    return pai[x];
}

vector<edge> grafo, mst;    // o grafo e a MST s�o armazenados como um vetor de arestas
int n;                      // n�mero de n�s do grafo

/*
 * Entrada: 'grafo': vetor de arestas que comp�em o grafo; 'n': n�mero de nodos do grafo.
 * Sa�da: a fun��o retorna o custo da MST; na vari�vel 'mst' guardam-se as arestas da �rvore geradora m�nima.
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

        // se 'a' e 'b' n�o est�o no mesmo conjunto (ou seja, adicionar essa aresta n�o formar� ciclo),
        // ent�o adicionar aresta na MST
        if(pa != pb)
        {
            custo += grafo[i].custo;
            pai[pa] = pb;
            mst.push_back(grafo[i]);
        }
    }

    // retornamos o custo da MST (em v�rios problemas apenas isso � pedido, e n�o a MST em si)
    return custo;
}
```
