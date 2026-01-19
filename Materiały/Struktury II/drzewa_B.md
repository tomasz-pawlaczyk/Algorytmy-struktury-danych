# B drzewa

B-drzewo to **zrównoważone drzewo wyszukiwań**, w którym każdy węzeł może przechowywać **wiele kluczy i wiele dzieci**.  
Jest szeroko stosowane w **systemach baz danych i systemach plików**, ponieważ minimalizuje liczbę operacji dyskowych.

---

## Właściwości B-drzew

- wszystkie liście są na **tym samym poziomie**
- klucze w węźle są **uporządkowane**
- struktura zawiera **k** kluczy, które należy do przedziału **[m, 2m]**
- struktura ma **k+1** wskaźników na dolne elementy
- operacje: wyszukiwanie, wstawianie, usuwanie → **O(log n)**

#### Definicje:

**Rząd B-drzewa** (`m`): minimalna liczba kluczy w każdej stronie (poza korzeniem); strona ma od **m do 2m kluczy

**Liczba `k`**: aktualna liczba kluczy zapisanych w danej stronie

<br>

![](../images/81478806211e48a2bc095ad34c5b22ebddb7f1f6.png)

<br>

Struktura:

```c
struct node
{
    int key[2m + 1];  // klucze indeksowane od 1, zerowy to wartownik
    node* next[2m + 1];
    int k;  // stopień
}
```

Wyszukiwanie rekurencyjne

```js
node* Search(node* root, int value)
{
    if (!root)
        return NULL;

    root->key[0] = -Infinity;
    int i = root->k;

    while (root->key[i] > value)
        i--;
    if (root->key[i] == value)
        return root;

    return Search(root->next[i], value);
}
```

Wizualizacja wstawiania `23` do pełnego drzewa:

Startowe drzewo

![](../images/05a3d350bf240eac42f950487d90853121fd2d7b.png)

Element `23` nie mieści się w root

![](../images/e3b4ae35147441fc69ee86307c859a1a4c9c27e0.png)

Wstawiamy do wskaźnika pomiędzy 20 a 30

![](../images/43d9329cf6960cefc3f30c69dd4202c8123b65b2.png)

Teraz struktura poniżej jest przeciążona

![](../images/bc978b2bd49f1e9feb2fa50dc6752440198a0895.png)

Środkowy element z przeciążonej struktury propagujemy do góry

![](../images/4349acdf37a1a8c27fc0164a88291d37811623a8.png)

Rozbijamy górny węzeł na 2 mniejsze, a aktualny środkowy element będzie je łączym 
i pełnił rolę root'a

![](../images/dbd201a62aa161cdee8c74a7978a491ef587bae4.png)

#### Usuwanie

Dodając - zawsze szliśmy w górę
Usuwając - zawsze idziemy w dół
