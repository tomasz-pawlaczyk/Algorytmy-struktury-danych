**Zrównoważone drzewa** to takie, których pesymistyczna złożoność wyszukiwania jest logarytmiczna, np. AVL, czerwono-czarne

**Drzewo idealnie zrównoważone** – wszystkie poziomy z wyjątkiem
ostatniego są zapełnione – nieefektywne operacje wstawiania i
usuwania

|           | przypadek pesymistyczy | wartość średnia |
| --------- |:----------------------:| --------------- |
| **BST**   | n                      | 1.39 * log(n)   |
| **AVL**   | 1.44 * log(n)          | log(n) + 0.25   |
| **Splay** | n                      | 3 * log(n)      |
| **2-3-4** | 2 * log(n)             | 1.002 * log(n)  |

**Stabilność algorytmu sortowania** jest określana jako zachowanie początkowego
porządku elementów o jednakowych kluczach

**Algorytm sortuje w miejscu** jeśli oprócz pamięci na dane algorytm wymaga
jedynie stałej ilości pamięci (np. na zmienne proste)
