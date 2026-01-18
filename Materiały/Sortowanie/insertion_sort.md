# Insertion sort – sortowanie przez wstawianie

Sortowanie polega na wstawianiu kolejnych elementów z części nieposortowanej 
w odpowiednie miejsce w części już posortowanej.

#### Właściwości

- złożoność czasowa:
  - **O(n²)** - pesymistyczna
  - **O(n)** - dla danych prawie posortowanych
- złożoność pamięciowa: **O(1)** sortowanie w miejscu
- algorytm **stabilny**

Przypomina to układanie kart w talii - przesuwamy tak długo, aż będzie posortowane

```c
void insertion_sort(int A[], int n)
{
    for (int i = 2; i < n+1; i++){
        int j = i - 1;
        int key = A[i];
        
        while (j >= 1 && A[j] > A[i]){
            A[j+1] = A[j];
            j--;
        }
    
        A[j+1] = key;
    }
}
```






