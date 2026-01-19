#### Zadanie 1

Zaimplementuj rotację występującą przy zstępującym wstawianiu do drzew CC

```c
void RotateLeft(node* &p)
{

}
```

#### Zadanie 2

Zaproponuj odpowiednią strukturę węzła B-drzewa i napisz funkcję dodawania do strony elementu wraz z prawym jego poddrzewem:
`void InsertToPageR(node * root, int &v, node *&pr).`
Uwzględnić ewentualny podział strony (patrz parametry funkcji).

(zakładamy, że root to poprawna strona i zajmujemy się tylko wstawianiem)

```c
void InsertToPageR(node* root, int &v, node* &pr)
{
    int i = root->k;

    // przesuwanie kluczy i wskaźników w prawo
    while (i >= 1 && root->key[i] > v){
        root->key[i+1] = root->key[i];
        root->child[i+1] = root->child[i];
        i--;
    }

    root->key[i+1] = v;
    root->child[i+1] = pr;
    root->k++;

    // jeśli nie ma przepełnienia – koniec
    if (root->k <= 2*m){
        pr = NULL;
        return;
    }

    // --- PODZIAŁ STRONY ---
    node* newPage = new node;
    newPage->k = m;

    // klucze prawej strony
    for (int j = 1; j <= m; j++){
        newPage->key[j] = root->key[j+m+1];
        newPage->child[j] = root->child[j+m+1];
    }
    newPage->child[0] = root->child[m+1];

    // klucz środkowy idzie w górę
    v = root->key[m+1];

    root->k = m;
    pr = newPage; // Prawe poddrzewo v to nowa strona
}
```

#### Zadanie 3

Praktyczna złożoność operacji w B-drzewie: **O(log₍b₎ n)**, gdzie **`b` = liczba dzieci strony** (rozgałęzienie)
