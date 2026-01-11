# B-drzewa

Rzędu m

Niech najpierw m = 2

| 5   | 7   | 8   |     |
|:---:|:---:|:---:| --- |

Każda strona od `m` do `2m` elementów
Jeśli `k`-elementów to `k+1`-wskaźników
Wszystkie liście na jednym poziomie

```cpp
struct node
{
    int key[2m];
    node* next[2m + 1];
    int k;  // ile elementów jest na stronie, k 
}
```
