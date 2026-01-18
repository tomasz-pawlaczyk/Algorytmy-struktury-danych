# Selection sort - sortowanie przez wybór

Sortowanie polega na wielokrotnym wybieraniu najmniejszego elementu
z nieposortowanej części tablicy i zamianie go z pierwszym elementem tej części.

#### Właściwości

- złożoność czasowa: **O(n²)** 
- złożoność pamięciowa: **O(1)** (sortowanie w miejscu)
- algorytm **niestabilny**
- ilość porównań nie zależy od uporządkowania danych



```c
void selection_sort(int A[], int n)
{
    for (int i = 1; i < n; i++){
        int A= i;

        for (int j = i+1; j < n+1; j++){
            if (A[j] < A[minimum])
                minimum = j;
        }

        int pomoc = A[i];
        A[i] = A[minimum];
        A[minimum] = pomoc;
    }
}
```


