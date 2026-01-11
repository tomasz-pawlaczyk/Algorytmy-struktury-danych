# Ćwiczenia nr 1

## Listy jednokierunkowe

Lista jednokierunkowa to dynamiczna struktura danych złożona z elementów (węzłów), z których każdy zawiera wartość oraz wskaźnik na następny element. Umożliwia szybkie wstawianie i usuwanie w dowolnym miejscu listy, ale dostęp do elementów wymaga przechodzenia jej od początku, więc wyszukiwanie trwa O(n).

![](C:\Users\tomas\Pictures\Screenshots\Zrzut%20ekranu%202025-11-29%20110630.png)

Tworzenie elementu:

```cpp
struct element
{
    int value;
    element* next;
} *head = NULL
```

Wypisz wszystkie:

```cpp
void Print_all()
{
    auto p = head;
    while (p != NULL)
    {
        cout << p->value;
        p = p->next;
    }    
}
```

Wstaw element na początek:

```cpp
void Insert_front(int value)
{
    element* p_new = new element();
    p_new->value = value;
    p_new->next = NULL;
    head = p_new;
}
```

Wstaw element na koniec:

```cpp
void Insert_last(int value)
{
    element* nowy_el = new element();
    nowy_el->value = value;

    if (head == NULL)
    {
        head = p_new;
        return;
    }

    element* obecny = head;
    while (obecny->next != NULL)
    {
        obecny = obecny->next;
    }
    obecny->next = nowy_el;
}
```

Usuń i zwróć pierwszy element

```cpp
element* Delete_first()
{
    element* obecny = head;
    if (head == NULL)
        return NULL;

    head = head->next;
    obecny->next = NULL;
    return obecny;
}
```

Usuń i zwróć największy element

```cpp
element* Delete_max()
{
    element* obecny = head;
    element* poprzedni = NULL;
    element* maksymalny = head;
    element* przed_maksymalnym = NULL;

    while (obecny != NULL)
    {
        if (obecny->value > maksymalny->value)
        {
            maksymalny = obecny;
            przed_maksymalnym = poprzedni;
        }
        poprzedni = obecny;
        obecny = obecny->next;
    }

    // Jeśli maksymalny był na początku listy
    if (przed_maksymalnym == NULL)
        head = head->next;

    // Jeśli maksymalny był w środku lub na końcu
    else
        przed_maksymalnym->next = maksymalny->next;

    maksymalny->next = NULL;
    return maksymalny;    
}
```

Wstawianie do listy uporządkowanej:

```cpp
void Insert_to_ordered_list(int value)
{
    element* nowy_element = new element(value);

    if (head->next == NULL)
    {
        head->next = nowy_element;
        return;
    }

    if (head->value > nowy_element->value)
    {
        nowy_element->next = head;
        head->next = nowy_element;
    }

    element* obecny = head;
    while (obecny->next != NULL && obecny->next->value < value)
    {
        obecny = obecny->next;
    }

    nowy_element->next = obecny->next;
    obecny->next = nowy_element;
}
```

II sposób:

```cpp
// II sposób - wskaźnik na wskaźnik
void Insert_to_ordered_list(int value)
{
    element* nowy_element = new element(value);
    element** obecny = &head;

    while (*obecny != NULL && *obecny->value < value)
    {
        obecny = &(*obecny->next);
    }

    nowy_element->next = *obecny;
    // to co wcześniej wskazywało na większy element teraz 
    // wskazuje na nowy_element
    *obecny = nowy_element;  
}
```

Przykład działania:

**`head`**->**`3`**  -> **`7`** -> **`12`**

Pętla działa aż do 
`obecny == &(head->next)` - adres do wskaźnika na element **`7`**

Następnie:

`nowy->next = *obecny` = **7**

`*obecny = nowy_element` czyli to co wcześniej wskazywało na większy element
teraz wskazuje na **nowy_element**