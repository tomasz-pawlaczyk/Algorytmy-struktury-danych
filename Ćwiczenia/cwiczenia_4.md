# Ćwiczenia 4

### 1. Kopiec cd - budowanie

ilość operacji

T = 

Metody budowania kopca:

1. Wstawianie elementów w odpowiednie miejsca - **n * log(n)**

2. Wstawianie elementów tak jak idzie, a następnie poprawiamy downheap - **n**

**Kopiec - właściwości**

Minus: wyszukiwanie elementu, trzeba przejrzeć wszystkie elementy

### 2. Dwukopiec

<img src="https://ece.uwaterloo.ca/~dwharder/aads/Algorithms/Beaps/images/beap.03.png" title="" alt="Bi-parental Heaps (Beaps) | Algorithms and Data Structures | University of  Waterloo" width="415">

**Właściwości:**

- wysokość dwukopca to **√n**

- pola przechowują (wartość, kolumnę, wiersz)

Możemy używać na kolosie funkcji

- int ij2k(int i, int j){}    

- (int, int) k2ij(int k){}

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
        if ( A[k] < value){
            i--;
            j--;
            k = ij_to_k(i,j);
            continue;
        }
        
        if( n >= ij_to_k(i+1, j)){
            i = i + 1;
            k = ij_to_k(i,j);
        }
        else
            j = j - 1;
            k = ij_to_k(i, j);
        }
    }
}
```

### Kopiec lewostronny i skośny

<img src="https://eduinf.waw.pl/inf/alg/001_search/images/0113_01.gif" title="" alt="Algorytmy i Struktury Danych - Kopiec" width="265">

```cpp
void Insert(int value){
    node *p = new node(value, NULL, NULL, 0); //to zero to npl
    root = Union(root, p);
}
```

```cpp
void Delete_Max(int value){


}
```

**Podstawowe funkcje** to Insert() oraz Delete_Max()

Złożoność operacji **Union()**

|                    | złożoność pesymistyczna | złożoność zamortyzowana |
| ------------------ | ----------------------- | ----------------------- |
| kopiec lewostronny | O(log n)                | O(log n)                |
| kopiec skośny      | O(n)                    | O(log n)                |
