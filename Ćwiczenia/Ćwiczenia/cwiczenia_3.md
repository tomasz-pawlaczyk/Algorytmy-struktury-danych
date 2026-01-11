# Ćwiczenia nr 3

### Wieże Hanoi

Chcemy przenieść krążki z *source* na *destination*

```c++
void Hanoi(int n, int source, int destination, int help){
    if (n > 0){
        Hanoi(n-1, source, help, destination);
        MOVE(source -> destination);
        Hanoi(n-1, help, destination, source);
    }
    return 0;
}
```

Wersja iteracyjna

```cpp
void Hanoi(){
    int n = ___;
    int source = 1, help = 2, destination = 3;
    STACK S;

    |start| 
    if (n > 0){
        S.push(n, source, help, destination);
        n = n - 1;
        help <--> destination;
        S.push(etykieta1)        # etykieta to linijka MOVE(source->dest)

        go to |start|
    }

    etykieta_1 { 
        move(source -> destination);
        S.push(n, source, help, destination); 
        n = n - 1;
        help <--> source;
        S.push(etykieta_2);

        go to |start|
    }

    etykieta_2 {
        ( ... )
    }

    if (!S.is_empty()){
        (n, source, destination, help) = S.pop();
        etykieta = S.pop();       # pobieramy etykietę z pop(): 1 lub 2

        go to |etykieta|
    }

}
```

<br/><br/>

### Kopiec / Heap (tablicowo)

Jest to drzewo, które ma po lewej więcej elementów niż po prawej

![Java - Data Structure - Binary Heap : frhyme.code](https://upload.wikimedia.org/wikipedia/commons/thumb/d/d9/Complete_binary2.svg/440px-Complete_binary2.svg.png)

**up_heap()**

- Wstaw nowy element na koniec kopca.

- Porównaj go z jego rodzicem.

- Jeśli narusza własność kopca (np. jest większy w kopcu maksymalnym), zamień z rodzicem.

- Powtarzaj, aż element znajdzie właściwe miejsce lub trafi do korzenia.
  
         10                        10                          12
        /  \                      /  \                        /  \
       7    9                    7    12                     7    10
      / \  /                    / \   /                     / \   /
      3 5 12                   3   5  9                    3   5 9

<br/>

Wstawianie nowego elementu do kopca w sposób uporządkowany

```cpp
void up_heap(int i)
{
    while (i>1) 
    {
        int rodzic = i/2;
        if (Tab[rodzic] >= Tab[i])
            break;

        Tab[rodzic] <--> Tab[i];
        i = rodzic;
    }
}


void insert(int value)
{
    Tab[++n] = value;
    up_heap(n);
}
```

<br/>

**down_heap()**

Jeżeli usunęliśmy największy element z korzenia, musimy naprawić kopiec. Przesuwamy się od góry do dołu funkcją ***down_heap()***
Dodajemy element mały na korzeń, następnie będzie on spadał w dół, zamieniając się z elementem większych z 2 dzieci. 

```cpp
// Przekazujemy 'i' jako arg, bo wtedy dziala od każdego elementu A[i]
// Jeśli od korzenia to i=1

void down_heap(int i, int n) { 
    while (true) {       # jest wiele punktów wyjścia, dlatego 'true'
        if (2*i > n){
            break;       # bo jest liściem
        }

        int i_max = 2 * i;

        if (2*i + 1 <= n && A[2*i] < A[2*i + 1]){
            i_max = 2*i + 1;    # sprawdzamy, które jest większe
        }        

        if (A[i] >= A[i_max]) {
            break;
        }
        A[i] <--> A[i_max];
        i = i_max;
    }
}
```

<br/>

Przykład użycia do budowy kopca:

```cpp
void build_heap(int A[], int n) {
    // startujemy od ostatniego węzła wewnętrznego (z min 1 dzieckiem)
    for (int i = n/2; i >= 1; i--) {
        down_heap(A, i, n);
    }
}

int main() {
    int A[11] = {0, 3, 1, 6, 5, 2, 4, 8, 7, 9, 0};  
    int n = 10;

    build_heap(A, n);
} 

// WYNIK: 9 7 8 5 3 4 6 1 2 0
```

**Kopiec - właściwości**
Minus: wyszukiwanie elementu, trzeba przejrzeć wszystkie elementy
