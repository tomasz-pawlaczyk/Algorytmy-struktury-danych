# Drzewa czerwono-czarne

![](C:\Users\tomas\AppData\Roaming\marktext\images\0ab6c2584ec6c6b8d4657d350553c85f38bda711.svg)

Właściwości:

- Każdy węzeł: czerwony lub czarny

- Korzeń czarny

- Liście (NIL) czarne

- Czerwony nie ma czerwonego dziecka

- Każda ścieżka ma tyle samo czarnych węzłów

Są one pochodną 2-3-4 drzew

Zamiania 2-3-4-drzew na czerwono-czarne:

![](../images/2ef1c8a0eaf4d235d418907fbb9ea2ac32ecfa2c.png) 

1. Najwyższy element jest czarny

2. Jeżeli na jednym poziomie jest kilka węzłów, to propagujemy w górę, aby otrzymać drzewo binarne

3. To co zeszło w dół jest czerwone

## Przykład tworzenia w związku z resztą struktur

#### 1. Mamy drzewo AVL

<img title="" src="../images/7dd02208ee575ba6817180f6110a13a03e58b15e.png" alt="" width="480">

#### 2. Odpowiada mu następujące 2-3-4-drzewo

<img title="" src="../images/59c3849f5e991303c83a821a6e4e6d22c419d027.png" alt="" width="435">

#### 3. Z 2-3-4-drzewa poprzez propagowanie poziomych elementów oraz kolorowanie od korzenia otrzymujemy następujące drzewo czerwono-czarne

<img title="" src="../images/a85f3cf068fd42effaaf57660e9480616558180d.png" alt="" width="359">

#### 4. Jak wyglądały wcześniejsze ruchy?

Mieliśmy w połowie taką strukturę - zwróć uwagę na lewą stronę

<img src="../images/f7b69fd1fa96a97d278678bd92da03ec1f16d841.png" title="" alt="" width="408">

Potem dodając węzęł **`1`**  musieliśmy zmienić kolory kierując się od góry

<img title="" src="../images/26d3ec79ce9c6cfa3de2ebc3963c2ba474777421.png" alt="" width="442">

Finałowe drzewo wygląda następująco

<img title="" src="../images/e576d8a188d18859bc0d6593e2e0e7f8a9bfbbd5.png" alt="" width="526">
