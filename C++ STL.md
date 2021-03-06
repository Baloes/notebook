# C++ Standard Template Library

A Standard Template Library (STL) é a biblioteca padrão do C++ que possui implementação de estruturas de dados (containers), métodos e algoritmos que ajudam bastante na maratona. A biblioteca é imensa e há bastante explicação/documentação sobre os métodos, então o propósito desse arquivo é colocar alguns links úteis e ilustrar alguns exemplos de uso da STL.

## Links

Explicações voltadas para programação competitiva:
https://www.topcoder.com/community/data-science/data-science-tutorials/power-up-c-with-the-standard-template-library-part-1/<br>
https://www.topcoder.com/community/data-science/data-science-tutorials/power-up-c-with-the-standard-template-library-part-2/#nontrivial<br>

Documentação de todos os métodos, explicando o que fazem, parâmetros, retorno, exemplo de código e complexidade:
http://www.cplusplus.com/reference/<br>
http://pt.cppreference.com/w/<br>

No menu à esquerda do cplusplus.com há um link para todas as bibliotecas, mas boa parte são pouco ou nunca usadas na maratona. As mais úteis são:
 - todas listadas sobre 'Containers' exceto "array" e "forward_list" (pelo menos eu nunca usei essas)
 - sobre 'Other', bibliotecas "algorithm", "string" e "utility"

## Código

Ao invés de incluirmos um por um todas as bibliotecas que quisermos usar, um jeito mais fácil é incluir a biblioteca "bits/stdc++.h", que inclui todas as bibliotecas padrão. Também adicionamos um  'using namespace std;' para não ter que ficar escrevendo 'std::' antes de qualquer função ou classe definida na std (alguém dirá que isso é má pratica de programação, mas na maratona pode).

``` c++
#include <bits/stdc++.h>
using namespace std;

```
A STL é implementada utilizando *templates*, que tornam a implementação genérica, permitindo que o programador especifique o tipo desejado no código. Para isso especificamos o tipo entre chaves (podendo inclusive usar tipos próprios ou outros tipos da STL):

``` c++
vector<int> v;                   // um 'vector' de inteiros
vector<int> v[100];              // um vetor de 100 'vectors' de inteiros
vector< vector<int> > v;            // um 'vector' onde cada elemento é um 'vector' de inteiro
map< pair<int,int>, set<int> > m;   // um mapa cuja chave é um 'pair<int,int>' e cujo elemento mapeado por cada chave é um 'set<int>'

struct edge {
   int origem, destino, custo;
}

vector<edge> lista_arestas;
```

Pair<T1,T2> é um tipo que une dois tipos de dados (ou mais, se 'encadearmos' pair dentro de pair). Eles são muitas vezes mais práticos que declarar uma struct pois já tem implementado funções de comparação como '<' e '=='. No caso do operador '<' (e derivados), a comparação utiliza o primeiro elemento do pair para determinar o menor, e, em caso de empate no primeiro, utiliza o segumento elemento do pair.

``` c++
// declarando e encadeando pairs
pair<int,int> p;
pair<string, pair<int,int> > p3;

// acessando os valores
string s = p3.first;
int x = p3.second.first;
int y = p3.second.second;

// alterando os valores
p = make_pair(15, 15);
p3.first = "string";

// se quisermos ordenar uma lista de pontos por x e, em caso de empate, por y, basta guardar os pontos
// como um pair<int,int> onde .first é o x e .second é o y e usar a função sort
   // x,  y
pair<int,int> pontos;
sort(pontos, pontos + n);

// quando encadeamos pairs, um truque útil é utilizar #define para simplificar o modo como referenciamos
// os elementos (mas tome cuidado ao usar #define - o compilador irá substituir toda aparição de 'nome'
// por 'first', 'idade' por 'second.first' e assim por diante, ou seja, se você escrever 'int idade;' no
// código abaixo teria um erro de compilação bem pouco óbvio)

#define nome first
#define idade second.first
#define altura second.second

pair<string, pair<int,int> > pessoa;
pessoa.nome = "Bob";

```
Vector&lt;T&gt; é apenas um vetor padrão como os do C, mas com algumas funcionalidades a mais; por exemplo, você não precisa se preocupar com o tamanho de um vector, pode ir adicionando elementos e, se necessário, o Vector aumenta seu tamanho. Isso é bem útil quando não conhecemos o tamanho do vetor a priori, por exemplo para declarar um grafo por lista de adjacência.
``` c++
vector<int> grafo[100];  // repare que estamos declarando 100 vectors, um para cada nó

grafo[0].push_back(3);   // insere uma aresta do nó 0 para o 3 (0->3)
int viz = grafo[5][0];   // pega o primeiro vizinho do nó 5 (cuidado: o elemento 0 existe?)

                          // itera por todos os vizinhos do nó 0 e imprime eles
for(auto viz : grafo[0])  // esse tipo de 'for' (range-based for) existe só no C++11 em diante
 printf("%d ", viz);

```
Set&lt;T&gt; é um container que armazena elementos do tipo T de forma ordenada, permitindo inserir, remover e consultar elementos em O(log N) (internamente o Set é implementado como uma árvore balanceada). O set não armazena elementos repetidos (se chamar insert com um elemento já existente, o set não é alterado); isso muitas vezes é util, por exemplo se queremos determinar o número de elementos distintos em um vetor. Se for necessário guardar elementos repetidos, podemos usar um multiset&lt;T&gt;.

``` c++
set<int> s;
s.insert(10);
s.erase(15);
printf("%d\n", s.lower_bound(8));	// imprime o menor valor maior ou igual a 8 no set
if(s.count(10))
  printf("Tem o 10!");

for(auto i : s)		// itera pelos elementos de forma ordenada (por padrão, ordem crescente)
  printf("%d ", i);
```

``` c++
// solução do problema URI 2174 usando set

#include <bits/stdc++.h>
using namespace std;

int main()
{
    string nome;
    set<string> s;
    int n;

    cin >> n;
    while(n--)
    {
        cin >> nome;
        s.insert(nome);
    }

    cout << "Falta(m) " << 151 - s.size() << " pomekon(s).\n";

    return 0;
}

```

Map<T1, T2> é um container que mapeia chaves do tipo T1 para valores do tipo T2. Um map é como um set<T1>, mas além de armazenar as chaves do tipo T1, cada chave faz referência a um valor do tipo T2. Assim como no set, no map as chaves tem que ser distintas; já no multimap podemos ter várias chaves com o mesmo valor.

``` c++
map<string, int> m;
m["Bob"] = 5;
m["Alice"] = 20;

printf("%d\n", m["Bob"]);    // imprime 5
printf("%d\n", m["Alala"]);  // cuidado com o operador []; se a chave pesquisada não existir no map, ele vai criar
                             // um novo elemento com um valor padrão (por exemplo, nesse caso ele imprimiria 0),
                             // aumentando o tamanho do map
if(m.count("Alala") == 0)
  printf("Nao tem chave Alala\n");

for(auto i : m)		// itera pelos elementos imprimindo chave e valor (ordenados pela chave)
  cout << "Chave: " << i.first << "; valor: " << i.second << endl;

```

``` c++
// exemplo de um uso útil do map: transformar entradas com strings em inteiros

map<string,int> nomes;
int id = 0;

int get_id(string s)
{
    if(nomes.count(s))
        return nomes[s];
    nomes[s] = id;
    return id++;
}

...

for(int i = 0; i < m; i++)
{
    scanf("%s %s", nome1, nome2);

    int id1 = get_id(nome1);
    int id2 = get_id(nome2);

    grafo[id1].push_back(id2);
    grafo[id2].push_back(id1);
}

```
No C++11, temos ainda o unordered_set e unordered_map, que possuem as mesmas funcionalidades mas, ao invés de usar uma árvore binária balanceada, usam uma tabela hash. Assim, eles geralmente são um pouco mais rápidos que o set e o map, mas não armazenam os elementos de forma ordenada e então não permitem realizar buscas por um lower_bound ou upper_bound (por exemplo, se quisermos iterar por todos os elementos >= A e/ou <= B, isso é possível com set mas não unordered_set, a não ser que iterássemos por todos elementos).

Por fim, alguns exemplos de funções úteis da biblioteca &lt;algorithm&gt;:
``` c++
fill(v, v + n, 0);   // preenche o vetor 'v' das posições 0 até n-1 com valor 0
sort(v, v + n);      // ordena o vetor
lower_bound(vis, v + n, 15);  // faz uma busca binária e retorna o lower_bound (menor x >= 15) de 15 no vetor 'v' (vetor deve estar ordenado)
upper_bound(vis, v + n, 15);  // faz uma busca binária e retorna o upper_bound (menor x > 15)  de 15 no vetor 'v' (vetor deve estar ordenado)

min(10, 20);            // retorna o menor dos dois valores
min(10, min(20, 30));   // retorna o menor dos três
swap(a, b);             // troca o valor das variáveis 'a' e 'b'

void gera_todas_permutacoes(int *v, int n)
{
    sort(v, v + n);
    do {
        ...
    } while(next_permutation(v, v + n));
    // 'next_permutation' gera a próxima permutação de v em ordem lexicográfica;
    // no caso, esse while gera todas as permutações do vetor v
}
```