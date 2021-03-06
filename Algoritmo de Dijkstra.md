# Algoritmo de Dijkstra

O algoritmo de Dijkstra é um algoritmo que encontra o menor caminho entre vértices em um grafo com arestas de pesos não-negativos. O algoritmo calcula a menor distância a partir de um vértice inicial A para todos os outros, mas se estivermos interessados apenas na distância de A para B, podemos encerrar a busca assim que a menor distância até B tiver sido determinada.

O algoritmo explora o grafo de modo similar à BFS, mantendo um vetor que armazena a menor distância já encontrada para todos os demais (inicialmente, essa distância é 0 para o vértice inicial e INF, um valor grande, para todos os demais). A principal diferença é na forma como escolhemos o próximo nó a ser explorado: enquanto na BFS simplesmente pegamos o próximo nó na fila, no algoritmo de Dijkstra escolhemos o vértice com menor distância entre os ainda não processados. Em cada iteração, ao selecionarmos o vértice de menor distância, determinamos que essa distância é a menor possível para aquele vértice (uma vez que as arestas são não negativas). Então atualizamos a menor distância para seus vizinhos, comparando a menor distância armazenada no vetor com a distância passando pelo vértice atual (custo até vértice atual + custo da aresta até vizinho). Para determinar de forma eficiente qual vértice escolher em cada iteração, usamos uma fila de prioridade (heap).

![Exemplo](http://2.bp.blogspot.com/-zog-0TI1lhs/U_-LvZysNwI/AAAAAAAABkQ/3Rz0Zqgm8bM/s1600/dij.png)

## Links

https://en.wikipedia.org/wiki/Dijkstra%27s_algorithm<br>
https://youtu.be/o4wv-OjMkj0?t=37m8s<br>
http://noic.com.br/informatica/curso-noic-de-informatica/aula-10-grafos-iii-menor-caminho/<br>

## Problemas

https://www.urionlinejudge.com.br/judge/pt/problems/view/1123<br>
https://www.urionlinejudge.com.br/judge/pt/problems/view/1148<br>
https://www.urionlinejudge.com.br/judge/pt/problems/view/2359<br>
http://olimpiada.ic.unicamp.br/pratique/programacao/nivel2/2009f1p2_pontes<br>

## Código

``` c++

/* Alguns comentários:
 * INF é um número grande, geralmente 10^9 basta (e 1001001001 é fácil de ver se está com o número certo de dígitos)

 * Para a fila de prioridade, no C++, usamos uma priority_queue de pair<int,int>; esse par significa (distância, id do nó)
    (ou seja, se o custo for um double, vira pair<double, int>, ou talvez pair<long long,int>, e assim por diante).

 * Por padrão, a priority_queue coloca no topo os elementos de maior valor; por isso, na declaração incluimos os parâmetros
    vector<...> e greater<...> para que coloque os menores valores no topo. Mas um outro truque comum é usar a priority_queue com
    o operador padrão e sempre colocar o valor negativo da distância na fila, desta forma as menores distâncias ficam no topo.

 * Para armazenar grafos com pesos nas arestas, podemos usar uma lista de adjacência mas, ao invés de apenas guardar o
    destino de cada aresta, guardamos um par (destino, custo).

 * No laço 'for' dentro do 'while', temos que iterar por todos os vizinhos de 'atual'; se estivermos usando a representação
    do grafo com lista de adjacência no 'vector', um jeito prático de fazer isso no C++11 é usando a sintaxe
        for(auto [var] : [vector])
    que itera por todos os elementos de [vector] com a variável [var].

 * No código abaixo, apenas retornamos o custo do menor caminho de 'ini' a 'fim'. A menor distância de 'ini' para todos os outros
    vértices estará no vetor 'dist', mas aí temos que remover o "if(atual == fim) return custo" para o algoritmo rodar até o final.

 * Na maioria dos problemas, apenas a menor distância entre os vértices basta. Se quisermos o caminho de menor distância,
    precisamos de outro vetor 'pai' onde pai[i] é o nó predecessor de i no menor caminho até i; ou seja, toda vez que
    atualizamos a distância para i, atualizamos seu pai, e depois reconstruimos o menor caminho de trás pra frente (começando
    no nó destino, seguindo para seu pai, depois para o pai de seu pai, e assim por diante até chegar no nó inicial).
*/

#define INF 1001001001

vector< pair<int,int> > grafo[MAXN];
int n;
int dist[MAXN];

/*
 * Entrada:
 *   - variáveis globais: 'grafo': lista de adjacência com pares (destino, custo); 'n': número de nós do grafo;
 *   - parâmetros: 'ini', 'fim': vértices de início e fim do menor caminho desejado.
 * Saída: retorna o menor custo entre 'ini' e 'fim'.
 * Complexidade: O(E log E), onde E é o número de arestas do grafo.
 */

int dijkstra(int ini, int fim)
{
    typedef pair<int,int> pii;
    priority_queue<pii, vector<pii>, greater<pii> > pq;

    fill(dist, dist + n, INF);

    dist[ini] = 0;
    pq.push(make_pair(0, ini));

    while(!pq.empty())
    {
        int custo = pq.top().first;
        int atual = pq.top().second;
        pq.pop();

        if(atual == fim) return custo;
        if(custo != dist[atual]) continue;

        for(auto i : grafo[atual])
        {
            int peso = i.first;
            int viz = i.second;

            if(custo + peso < dist[viz])
            {
                dist[viz] = custo + peso;
                pq.push(make_pair(dist[viz], viz));
            }
        }
    }

    return -1;
}
```