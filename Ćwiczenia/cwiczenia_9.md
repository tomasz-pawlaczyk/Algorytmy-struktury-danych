# Ćwiczenia nr 8

## Splay - drzewa samoorganizujące się

Drzewo Splay jest samoorganizującą się strukturą, gwarantującą efektywny dostęp do pól danych na podstawie częstotliwości ich pojawiania się.

Właściwości:

- łożoność pesymistyczna: O(n)

- złożoność zamortyzowana: O(log n)

Wizualizacja funkcji **Splay(5)**

![](images/bec0b36636a2219db9d2e73b11e684e4a24ca71e.png)

```cpp
void Splay(node* &root, int value)
{
    node* p = root;

    [co tu dopisać?]

    while (p->parent != NULL)
    {
        node* dziadek = p->parent;
        if (dziadek->parent)
            dziadek = dziadek->parent;

        int i = where_is(p, dziadek);
        switch (i)
        {
            case 1:
                Lzigzag(dziadek);
                break;
            case 2:
                Lzigzag(dziadek);
                break;
            ...

        }

    }
    root = p;
}
```

Sposoby cofania się w drzewach:

- dodanie do `node` parametru *parent*

- dodawanie kolejnych elementów na stacka (stos)

- rekurencyjnie

Szukanie

```cpp
node* Search(int value)
{
    Splay(root, value);
    if (root->key == value)
        return root;
    return NULL;
}
```

Wstawianie

```cpp
node* Insert(int value)
{
    Splay(root, value);
    if (root->key == value)
        return root;

    node* nowy = new node(value);
    if (root->key < value) {
        nowy->left = root;
        nowy->right = root->right;
        root->right = NULL;
        root = nowy;
    }
    else {
        (symetrycznie)
    }
    return nowy;    
}
```

Usuwanie - DOKOŃCZ

```cpp
void Delete(value)
{
    Splay(root, value);
    (zapamietujemy lewe poddrzewo)

    if (root->key == value)
        // Używamy prawego poddrzewa
        Splay(root->right, value);   // bez wzgl zwróci nam najmniejsze

        root->(dolaczamy zmodyfikowane prawe poddrzewo)


}
```

## Drzewa RST

Są to drzewa wyszukiwań pozycyjnych (Radix Search Tree)

Mamy `key`:

| 0        | 1        | 2        | 3        | 4        | 5        |
|:--------:|:--------:|:--------:|:--------:|:--------:|:--------:|
| [0, k-1] | [0, k-1] | [0, k-1] | [0, k-1] | [0, k-1] | [0, k-1] |
