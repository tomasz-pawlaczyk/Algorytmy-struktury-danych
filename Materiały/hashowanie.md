# Hashowanie

Funkcje zwykłe:

```c
bool Search(int v) {  
    return A[v];  
}  

void Insert(int v)  {
    A[v] = true; 
} 

void Delete(int v) { 
    A[v] = false; 
}
```

Funkcje z hashowaniem:

```c
int Search(int v) 
{
    int i = h(v);
    if (A[i]==v)
        return i;
    else
        return -1;
}

void Insert(int v) {
    A[h(v)] = v;
}

void Delete(int v) {
    A[h(v)] = -1;
}
```

## Mieszanie łańcuchowe

- tablica przechowuje **wskaźniki do list** elementów  
- elementy z tą samą wartością funkcji haszującej trafiają do **jednej listy**  
- kolizje są rozwiązywane przez **dopisywanie elementów do listy**  

#### Złożoności

- pesymistyczna: **O(n)** (wszystkie elementy w jednej liście)  
- średnia: **O(n/m)**  
- dla `n ≤ m`: **O(1)**  

#### Pamięć

- złożoność pamięciowa: **O(n + m)**  - suma wezłów i rozmiaru tablicy
- dodatkowa pamięć na **wskaźniki w listach**

---

## Mieszanie otwarte

- wszystkie elementy przechowywane są **bezpośrednio w tablicy**
- brak list i dodatkowych wskaźników
- kolizje rozwiązywane przez **szukanie innego pola w tablicy**

#### Metody

- **mieszanie liniowe**: kolejne pola `h(v), h(v)+1, ...`
  słabe, ponieważ powstają grupy wartości w tablicy
- **mieszanie podwójne**: `h(v) + k · h1(v)`

#### Właściwości

- wymaga oznaczania pól: **wolne / zajęte / usunięte**
- złożoność pamięciowa: **O(m − n)**
- wydajność spada, gdy **n zbliża się do m**
- wyszukiwanie kończy się po napotkaniu **wolnego pola**

Szukanie z użyciem mieszania otwartego liniowego

```c
int Search(int value)
{
    int i = hash(value);
    while (H[i] != FREE)
    {
        if (H[i] == value)
            return i;
        i = (i + 1) % M;
    }
    return -1;
}
```

Wstawianie z użyciem mieszania otwartego liniowego

```c
int Insert(int value)
{
    int i = hash(value);
    while (H[i] != FREE)
    {
        if (H[i] == value)
            return i;
        i = (i + 1) % M;
    }
    H[i] == value;
    return i;
}
```
