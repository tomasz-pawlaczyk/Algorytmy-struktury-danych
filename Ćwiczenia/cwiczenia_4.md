# Ćwiczenia 4

### Dwukopiec

<img src="https://ece.uwaterloo.ca/~dwharder/aads/Algorithms/Beaps/images/beap.03.png" title="" alt="Bi-parental Heaps (Beaps) | Algorithms and Data Structures | University of  Waterloo" width="415">

**Właściwości:**

- wysokość dwukopca to **√n**

- pola przechowują (wartość, wiersz(i), kolumnę(j))

Możemy używać na kolosie funkcji

- **int ij2k(int i, int j){}**   

- **(int, int) k2ij(int k){}**

W dwukopcu zaczynamy szukanie od ostatniego elementu pełnego wiersza
Będziemy kierować się od tego elementu na zachód. 
Gdy nasz element jest większy to północ, gdy mniejszy to południe.

```c++
int Search(int value){
    (int i, int j) = k_to_ij(n);

    if (i != j){
        i = i - 1;
        j = i;
    }

    int k = ij_to_k(i, j);

    while (j > 0 && A[k] != value){
        // Obecny mniejszy - idź lewo, góra
        if ( A[k] < value){
            i--;
            j--;
            k = ij_to_k(i,j);
            continue;
        }
        
        // Obecny większy - idź w lewy dół, lewe dziecko
        else if( n >= ij_to_k(i+1, j)){     // A[k] >= value
            i = i + 1;
            k = ij_to_k(i,j);
        }
        
        // Nie ma dziecka - idź na lewo
        else
            j = j - 1;
            k = ij_to_k(i, j);
        }
    }
}
```

<br/>

## Kopiec lewostronny

<img src="https://eduinf.waw.pl/inf/alg/001_search/images/0113_01.gif" title="" alt="Algorytmy i Struktury Danych - Kopiec" width="265">

<br/>

Każdy element ma wskaźniki na prawe i lewe dziecko oraz liczbę **NPL**, która określa odległość od liścia

Deklaracja:

```cpp
struct node
{
    int value;
    node* left, node* right;
    int npl;  // null path lenght

    node(int v, node* l=nullptr, node* r=nullptr, int n=0)
        : value(v), left(l), right(r), npl(n) {}
}
```

```cpp
void Insert(int value){
    node *p = new node(value, NULL, NULL, 0); //to zero to npl
    root = Union(root, p);
}
```

```cpp
void Delete_Max(int value){
    int maxValue = root->value;

    node* left = root->left;
    node* right = root->right;

    delete root;

    root = Union(left, right);
    return maxValue;
}
```

```cpp
node* Union(node* a, node* b)
{
    if (a->value < b->value)
        a <--> b;

    a->right = Union(a->right, b);

    if (!(a->left) || a->left->npl < a->right->npl)
        a->left <--> a->right;

    // Aktualizacja NPL
    if (a->right)
        a->npl = a->right->npl + 1;
    else
        a->npl = 0;

    return a;
}
```

<br/>

**Podstawowe funkcje** to Insert() oraz Delete_Max()

Złożoność operacji **Union()**

<br/>

## Kopiec skośny

To samo co lewostronny, ale bez NPL

<br/>

## Porównanie kopca lewostronnego i skośnego

|                            | Lewostronny                                     | Skośny                          |
|:--------------------------:|:-----------------------------------------------:|:-------------------------------:|
| **Parametr**               | NPL                                             | brak                            |
| **Union()**                | lewe poddrzewo ma większy NPL                   | -                               |
| **Cecha**                  | Dzięki temu prawe poddrzewo jest jak najkrótsze | Brak gwarancji dobrej wysokości |
| **Wysokość pesymistyczna** | O(log n)                                        | O(n)                            |
| **Wysokość zamortyzowana** | O(log n)                                        | O(log n)                        |
