# Drzewa RST

S± to drzewa wyszukiwañ pozycyjnych (Radix Search Tree), w których klucze s± rozró¿niane na podstawie **kolejnych bitów klucza**.
Stanowi± prost± alternatywê dla drzew BST i dobrze sprawdzaj± siê w
przypadkach pesymistycznych.

**W³a¶ciwo¶ci:**

- na poziomie `i` sprawdzany jest **i-ty bit klucza**

- bit `0` - lewe poddrzewo, bit `1` - prawe poddrzewo

- brak porz±dku typu BST (lewe < korzeñ < prawe)

- maksymalna wysoko¶æ ograniczona **d³ugo¶ci± klucza**

**Z³o¿ono¶æ:**

- wyszukiwanie, wstawianie, usuwanie: **O(d)**, gdzie `d` = liczba bitów

- ¶rednia z³o¿ono¶æ operacji: **O(log n)**

![](../images/2a9f96ad1d6be5d7297beecda1045e83ffe28443.jpg)

Struktura

```c
struct node
{
    int key;
    node* left, right  // Albo: node* next[2]
}
```

Szukanie:

```c
node* Search_RST(int value)
{
    node* p = root; 
    int i = 4;      // aktualny nr bitu klucza
    while (p && p->key != value)
    {
        if (bit(value, i) == 0)
            p = p->left;
        else
            p = p->right;
        i = i - 1;
    }
    return p;
}
```

Wstawianie:

```c
void Insert(int value)
{
    node* nowy = new node(value);
    node* p = root;
    node* parent = NULL;
    int i = 4;

    while (p && p->key != value)
    {
        parent = p;
        if (bit(value, i) == 0)
            p = p->left;
        else
            p = p->right;
        i = i - 1;
    }

    if (p) {
        print("Warto¶æ ju¿ istnieje");
        delete(nowy);
        return;
    }

    if (bit(value, i + 1) == 0)    
        parent->left = nowy;
    else
        parent->right = nowy;
}
```

#### To samo, ale dwoma wska¼nikami

Szukanie, podwójny wska¼nik:

```c
node** Search_v2(int value)
{
    node** p = &root;
    int i = 4;

    while (*p && (*p)->key != value)
    {
        if (bit(value, i) == 0)
            p = &((*p)->left);
        else
            p = &((*p)->right);
    }
    return p;
}
```

Wstawianie, ale podwójny wska¼nik:

```c
void Insert_v2(int value)
{
    node** p = Search_v2(value);

    if (*p)
        print("Warto¶æ ju¿ istnieje");
        return;

    *p = new node(value);
    (*p)->left = NULL;
    (*p)->right = NULL;    
}
```

Usuwanie z podwójnym wska¼nikiem:

```c
void Delete_v2(int value)
{
    node** p = Search_v2(value);

    if (!*p){
        print("Nie ma co usun±æ");
        return;
    }

    // *p jest li¶ciem
    node* pomoc = *p;
    if (!pomoc->next[0] && !pomoc->next[1]) {
        *p = NULL;
        delete(pomoc);
        return;
    }

    // je¶li *p nie jest li¶ciem - znajd¼ dowolny li¶æ z poddrzewa
    node** podlisc = p;

    while ((*podlisc)->next[0] || (*podlisc)->next[1]) {
        int b;
        if ((*podlisc)->next[0] && (*podlisc)->next[1])
            b = rand() % 2;
        else if ((*podlisc)->next[0])
            b = 0;
        else
            b = 1;

        podlisc = &((*podlisc)->next[b]);
    }

    (*p)->key = (*podlisc)->key;

    node* kopia = *podlisc;  // Zapamiêtujê wska¼nik na wêze³
    *podlisc = NULL;         // Odpinam podli¶æ z drzewa
    delete(kopia);           // Zwalniam pamiêæ wêz³a na stercie
}
```

# Modyfikacja: drzewa reTRIEval

<img title="" src="../images/a28604a2f2da2e171a66c8f8d44b96d6a5b1ed91.png" alt="" width="466">

Szukanie:

```c
node* Search_retrieval(int value)
{
    node* p = root;
    int i = 4;
    while (p && (p->left || p->right))
    {
        if (bit(value, i) == 0)
            p = p->left;
        else    
            p = p->right;
        i = i - 1;
    }

    return (p && (p->key == value) ? p : NULL);
}
```

#### Podwójne wska¼niki

Wyszukiwanie z podwójnym wska¼nikiem
Nie zwraca miejsca gdzie powinna warto¶æ, bo nie ma w ogólno¶ci jednego poprawnego miejsca 

```c
node** Search_retrieval_v2(int value)
{
    node** p = &root;
    int i = 4;

    while (*p && ((*p)->left || (*p)->right)) 
    {
        if (bit(value, i) == 0) 
            p = &((*p)->left);
        else
            p = &((*p)->right);
        i = i - 1;
    }

    // Zwracamy tylko gdy znale¼li¶my warto¶æ
    return ((*p) && (*p)->key == value) ? p : NULL; 
}
```
