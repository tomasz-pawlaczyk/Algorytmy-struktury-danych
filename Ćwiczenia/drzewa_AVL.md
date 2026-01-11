# Drzewa AVL

![](images/addec12e5333fb26ea3edcde696ddae1a97b5d2a.png)

Właściwości:

- Jest to pochodna drzew BST - zachowane wartości mniejsze / większe

- Są one zrównoważone

- zawierają pole **```balans```**, które jest różnicą wysokości prawego i lewego podrzewa, powinno zawierać się w zbiorze {-1, 0, 1}

Są to drzewa gdzie dla każdego węzła wysokość podrzew różni się nie więcej niż o 1 poziom. 

Struktura węzła:

```c
struct node{
    int key;
    int balans;
    node* left, right;
}

ALBO: node* next[2];
```

Mogą wystąpić 4 typy nierówności

![](images/bd4982ffef746bd3df090dffd25f0e77d4af51fe.png)

**Rotacja Right-Left**

![](images/8828a4bc8925cafd40fe230542e27afab7e09906.png)

**Implementacja funkcji wyrównywania**

```c
void RL(node* &root)
{
    node* x = root;
    node* y = root->right->left;
    node* z = root->right;

    x->right = y->left;
    z->right = y->left;
    y->right = z;
    y->left = x;

    x->balans = 0;
    y->balans = 0;
    z->balans = 0;

    root = y;
}
```

(dodać wizualizację z zeszytu)
Warto zauważyć, że złożoność jest stała
