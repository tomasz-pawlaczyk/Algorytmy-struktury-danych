# Bubble sort – sortowanie bąbelkowe

Sortowanie polega na **wielokrotnym porównywaniu sąsiednich elementów**
i **zamianie ich miejscami**, jeśli są w złej kolejności.
Największe elementy „wypływają” na koniec tablicy.

#### Właściwości

- złożoność czasowa:
  - **O(n²)** - pesymistyczna
  - **O(n)** - dla danych już posortowanych
- złożoność pamięciowa: **O(1)** - sortowanie w miejscu
- algorytm **stabilny**



```c
void bubble_sort(int A[], int n)
{
    for (int i = 1; i < n; i++) {
        for (int j = 1; j < n-i+1; j++) {
            if (A[j] > A[j+1]){
                int pomoc = A[j];
                A[j] = A[j+1];
                A[j+1] = pomoc;
            }
        }
    }
}
```



# Cocktail Shaker Sort – sortowanie mieszane

Sortowanie polega na naprzemiennym przechodzeniu tablicy w prawo i w lewo.
Jest to ulepszona wersja bubble sorta, w której **największe elementy przesuwane są na koniec, a najmniejsze na początek** tablicy w jednym cyklu.

Naprawia przypadek `2`, `3`, `4`, `5`, `1` 

#### Właściwości

- złożoność czasowa:
  - **O(n²)** – pesymistyczna  
  - **O(n)** – dla danych już posortowanych  
- złożoność pamięciowa: **O(1)** – sortowanie w miejscu  
- algorytm **stabilny**
- zmniejsza zakres sortowania po każdym przejściu 

```c
void cocktail_shaker_sort(int A[], int n)
{
    int left = 1;
    int right = n-1;
    int k = left;

    do 
    {
        // Przejście w prawo
        for (int i = left; i <= right; i++) {
            if (A[i] > A[i+1]) {
                int pomoc = A[i];
                A[i] = A[i+1];
                A[i+1] = pomoc;
                k = i;
            }
        }
        right = k - 1;

        // Przejście w lewo
        for (int i = right; i >= left; i--) {
            if (A[i] > A[i+1]) {
                double pomoc = A[i];
                A[i] = A[i+1];
                A[i+1] = pomoc;
                k = i;
            }
        }
        left = k + 1;

    } while (left <= right);
}
```

# Comb Sort – sortowanie grzebieniowe

Comb Sort to **modyfikacja bubble sorta**, w której porównuje się elementy
oddalone o pewną odległość `gap`. Dzięki temu szybciej eliminowane są
małe elementy znajdujące się daleko od początku tablicy.

#### Właściwości

- porównuje elementy oddalone o `gap`
- po osiągnięciu `gap = 1` działa jak bubble sort
- zmienna `swapped` kontroluje, czy w danym przebiegu były zamiany
- algorytm **niestabilny**
- złożoność czasowa:
  - **O(n²)** – pesymistyczna  
  - ~**O(n log n)** – w praktyce
- złożoność pamięciowa: **O(1)** – sortowanie w miejscu

Jest to funkcja, która poprawia problem sortowania bąbelkowego polegający na przechodzeniu po elementach nawet jeśli ciąg jest już posortowany  

```c
void comb_sort(int A[], int n)
{
    int gap = n;
    bool swapped = true;

    while (gap > 1 || swapped)
    {
        gap = gap * 10/13;    // wyznaczone doświadczalnie
        if (gap == 0)
            gap = 1;

        swapped = false;

        for (int i = 1; i + gap <= n; i++){
            if (A[i+gap] < A[i]){
                int pomoc = A[i];
                A[i] = A[i+gap];
                A[i+gap] = pomoc;
                swapped = true;
            }
        }
    }
}
```






