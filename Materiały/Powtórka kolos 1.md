# Notatki ogólne

#### Zakres: kolokwium nr 1

<br/>

## Definicje

**Złożoność obliczeniowa** - ilość zasobów niezbędnych do wykonania algorytmu. Obejmuje to czas, pamięć operacyjną i liczbę operacji.

**Notacja Omega** - najlepszy możliwy czas działania 

**Notacja Theta** - dokładna złożoność, rośnie w tym czasie w najlepszym i najgorszym przypadku

**Złożoność średnia** - średni czas działania algorytmu obliczony po wszystkich danych wejściowych z uwzględnieniem ich prawdopodobieństwa

**Złożoność zamortyzowana** - średni koszt 1 operacji w dłuższej serii, gdzie niektóre operacje są rzadko bardzo drogie, ale większość jest tania

<br/>

|                 | Co oznacza?                                   | Trudność      |
|:---------------:|:---------------------------------------------:|:-------------:|
| **P**           | szybkie do wyliczenia                         | łatwe         |
| **NP**          | trudne do wyliczenia<br/>łatwe do sprawdzenia | trudne        |
| **NP-complete** | najtrudniejsze problemy NP                    | bardzo trudne |

<br/>

**Abstrakcyjne typy danych** - logiczny opis modelu danych. Uwgzlędnia dozwolone operacje, bez opisu implementacji
np. stos, kolejka

**Struktury implementacyjne** - konkretne struktury pamięci realizujące te poprzednie. Definiują pola, wskaźniki, operacje. 
np. tablica, lista jedno/dwukierunkowa, kopiec

<br/>

**Kopiec tablicowy** - przechowuje węzły w jednej ciągłej tablicy

**Kopiec wskaźnikowy** działa jak zwykłe drzewo binarne, ale trudniejszy w utrzymaniu struktury i zajmuje więcej pamięci przez wskaźniki

```cpp
// Tablica
Tablica = []*n;
rodzic = Tablica[i/2];
obecny = Tablica[i];
lewy = Tablica[2*i];
prawy = Tablica[2*i + 1];

// Wskaźniki
struct Node {
    int key;
    Node* left;
    Node* right;
};
```

<br/>

## Porównanie struktur

| Struktura                            | Insert() | Max_Element() | Delete_Max() | Union  | IncreaseKey() |
|:------------------------------------:|:--------:|:-------------:|:------------:|:------:|:-------------:|
| **Kolejka priorytetowa**             | n        | 1             | 1            |        |               |
| **Kopiec** (tablicowo)               |          |               |              |        |               |
| **Dwukopiec** (tablicowo)            |          |               |              |        |               |
| **Kopiec lewostronny** (wskaźnikowo) |          |               |              | log(n) |               |
| **Kopiec skośny** (wskaźnikowo)      |          |               |              | n      |               |
| **Kolejka dwumianowa**               | log(n)   | log(n)        | log(n)       | log(n) |               |
| **Kopiec Fibonaciego**               | 1        | 1             | log(n)       | 1      | 1             |
| Kopiec parujący                      | 1        | 1             | log(n)       | 1      | log(log(n))   |
| **2-3 drzewo**                       |          | log(n)        | log(n)       | log(n) |               |
|                                      |          |               |              |        |               |

<br/>

Dodatkowo IncreaseKey() dla kopca Fibonaciego wykonuje się w czasie stałym

<br/><br/><br/>
