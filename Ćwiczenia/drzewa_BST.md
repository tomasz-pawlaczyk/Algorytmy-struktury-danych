# Drzewa BST (binary search tree)

<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/d/da/Binary_search_tree.svg/1200px-Binary_search_tree.svg.png" title="" alt="Binary search tree - Wikipedia" width="310">

Własności:

- **```left```** mniejszy od rodzica, **```right```** większy od rodzica

Struktura węzła

```c
struct node{
    int key;
    node* left, right;
}

ALBO: node* next[2];
```

Szukanie elementu

```c
// Szukamy elementu o danej wartości oraz jego rodzica
// elem , rodzic
(node* , node*) szukaj(int value)
{
    if (root == NULL)        // ten warunek niepotrzebny, bo mamy while
        return (NULL, NULL);

    node* p = root;
    node* prev = NULL;
    while (p != NULL && p->value != value)
    {
        if (p->value > value)
        {
            prev = p;
            p = p->left;
        }
        else
        {
            prev = p;
            p = p->right;
        }
    }
    return (p, prev);
}
```

Wstawiamy element do drzewa:

```c
node* Insert(int value)
{
    (node* szukany, node* rodzic) = Search(value);
    if (szukany)
        return szukany;

    node* nowy = new node(value);
    if (!rodzic)
    {
        root = nowy;
        return nowy;
    }

    if (rodzic->key > value)
        rodzic->left = nowy;
    else
        rodzic->right = nowy;
    return nowy;
}
```

#### Podwójne wskaźniki

Inny sposób na wyszukiwanie, używając podwójnego wskaźnika

```c
node** Search_v2(int value)
{
    node** p = &root;
    while (*p != NULL && (*p)->key != value)
    {
        if ((*p)->key > value)
            p = &((*p)->left);
        else
            p = &((*p)->right);
    }
    return p;
}
```

Druga wersja ``Insert()`` wykorzystującą ``Search_v2()`` na podwójnym wskaźniku

```rust
node* Insert_v2(int value)
{
    node** p = Search_v2(value);
    if (*p)
        return (*p);

    node* nowy = new node(value);
    (*p) = nowy;
    return *p;
}
```

Ta funkcja jest poprawna, ponieważ  **nie zwraca węzła**, tylko **adres wskaźnika**, który:

- wskazuje na znaleziony **`element`** 
  
  lub

- wskazuje na **`miejsce`**, gdzie element powinien zostać wstawiony

Można napisać wstawianie na podwójnym wskaźniku bez Search_v2:

```c
node* Insert_manual(int value)
{
    node** p = &root;

    while (*p)
    {
        if ((*p)->key == value)
            return *p;

        if ((*p)->key > value)
            p = &((*p)->left);
        else
            p = &((*p)->right);
    }

    node* nowy = new node(value);
    *p = nowy;
    return nowy;
}
```

Funkcja usuwająca element z dwoma wskaźnikami

```c
void Delete(int value)
{
    node* do_usuniecia;
    node** pomoc;
    node** p = Search_v2(value);

    if(*p)
    {
        if ( (*p)->next[0] && (*p)->next[1] )
        {
            int b = losuj(left, right);
            pomoc = &( (*p)->next[b]);    // jeśli najpierw w prawo, 
            while( (*pomoc)->next[1-b] )  // to potem ciągle w lewo
                pomoc = &( (*pomoc)->next[1-b] );
            do_usuniecia = *pomoc;
            (*p)->key = do_usuniecia->key;
            *pomoc = do_usuniecia->next[b];  // jedyny możliwy potomek
        }     

        else   // ma 1 dziecko lub wcale
        {
            do_usuniecia = *p;
            // potencjalne dziecko zastępuje element usunięty
            *p = (*p)->next[(*p)->next[0] == NULL]
        }    

        delete do_usuniecia;
    }
}
```

## Złożoność pesymistyczna

W pesymistycznym przypadku wysokość drzewa to `n`, ponieważ elementy mogą być posortowane. Wtedy dla całości mamy `n*n`

## Złożoność średnia

Wstawienie pojedynczego elementu w losowym zbiorze zajmuje `log(n)`
Mamy docelowo `n` elementów
Zatem złożoność to średnia to `n*log(n)`
Można pokazać, że dla drzew BST współczynnik O-notacji wynosi **1.39**
