# QuickSort – sortowanie szybkie

QuickSort jest oparty na strategii dziel i zwyciężaj. Polega na wyborze elementu dzielącego (pivotu), podziale danych na dwie części oraz rekurencyjnym sortowaniu obu fragmentów w tej samej tablicy.

#### Właściwości

- złożoność czasowa:
  - **O(n²)** – pesymistyczna  
  - **O(n log n)** – średnia  
- złożoność pamięciowa: **O(log n)** – stos rekurencji  
- algorytm **niestabilny**
- bardzo szybki w praktyce
- silnie zależny od wyboru pivotu

#### Zamysł

def QuickSort(A) {
        if |A| == 1
                    return S
        else {
                    wybierz dowolny element `v` ze zbioru A
                    podziel zbiór A na A1, A2 aby elementem dzielącym był `v`
                    QuickSort(A1)
                    QuickSort(A2)
                    połącz A1 i A2
        }
}                            
    

Jak widać proces dzielenia na dwa zbiory jest wymagający.
Oto jego realizacja:

```c
int partition_1(int left, int right)
{
    double pivot = A[left];
    int i = left;
    int j = right + 1;

    do
    {
        do i++ while (A[i] < pivot);
        do j-- while (A[j] > pivot);
        if (i < j) {
            double pomoc = A[i];
            A[i] = A[j];
            A[j] = A[i];
        }
    } while (i < j);

    A[left] = A[j];
    A[j] = pivot;
    return j;
}
```

Inny sposób łączenia

```c
int partition_2(int left, int right)
{
    double pomoc;
    double pivot = A[right];
    int i = left - 1;

    for (int j = left; j <= right-1; j++) {
        if (A[j] <= pivot) {
            i++;
            pomoc = A[i];
            A[i] = A[j];
            A[j] = pomoc;
        }
    }

    pomoc = A[i+1];
    A[i+1] = A[right]; // pivot
    A[right] = pomoc;

    return i+1;
}
```
