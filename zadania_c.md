
# Zadania z języka C – wskaźniki, tablice, funkcje

## 3.2.1 – Zwracanie mniejszej wartości

```c
int mniejsza_wartosc(int* a, int* b) {
    return (*a < *b) ? *a : *b;
}
```

## 3.2.2 – Zwracanie wskaźnika na mniejszą wartość

```c
int* wsk_mniejsza(int* a, int* b) {
    return (*a < *b) ? a : b;
}
```

## 3.2.3 – Zamiana wartości przez wskaźniki

```c
void zamien(int* a, int* b) {
    int temp = *a;
    *a = *b;
    *b = temp;
}
```

## 3.2.4 – Zamiana jeśli pierwsza wartość mniejsza

```c
void zamien_jezeli_mniejsza(int* a, int* b) {
    if (*a < *b) {
        int temp = *a;
        *a = *b;
        *b = temp;
    }
}
```

## 3.2.5 – Suma przez wskaźniki do stałych

```c
int suma_stalych(const int* a, const int* b) {
    return *a + *b;
}
```

## 3.2.6 – Przypisanie wartości przez wskaźnik

```c
void przypisz(int d, int* w) {
    *w = d;
}
```

## 3.2.9 – Rezerwacja pamięci dla int

```c
int* rezerwuj_int() {
    return (int*)malloc(sizeof(int));
}
```

## 3.2.10 – Rezerwacja pamięci dla double

```c
double* rezerwuj_double() {
    return (double*)malloc(sizeof(double));
}
```

## 3.2.11 – Rezerwacja tablicy int

```c
int* rezerwuj_tablice_int(int n) {
    return (int*)malloc(n * sizeof(int));
}
```

## 3.2.12 – Rezerwacja tablicy double

```c
double* rezerwuj_tablice_double(int n) {
    return (double*)malloc(n * sizeof(double));
}
```

## 3.2.13 – Funkcja przyjmująca funkcję i liczbę

```c
double zastosuj_funkcje(double (*f)(int), int x) {
    return f(x);
}
```

## 3.2.14 – Porównanie wartości zwróconych przez funkcję

```c
int porownaj_wartosc_funkcji(int (*f)(int), int x, int y) {
    return f(x) == f(y);
}
```

## 3.2.15 – Przypisanie wartości ze stałej

```c
void przypisz_wartosc(const int* zrodlo, int* cel) {
    *cel = *zrodlo;
}
```

## 3.2.16 – Przypisanie przez wskaźnik na wskaźnik

```c
void przypisz_zmienna(int* const* zrodlo, int* cel) {
    *cel = **zrodlo;
}
```

## 4.2.1 – Operacje na tablicach

```c
void zeruj_tablice(int n, int* tab) {
    for (int i = 0; i < n; ++i)
        tab[i] = 0;
}

void indeksuj_tablice(int n, int* tab) {
    for (int i = 0; i < n; ++i)
        tab[i] = i;
}

void podwajaj_tablice(int n, int* tab) {
    for (int i = 0; i < n; ++i)
        tab[i] *= 2;
}

void wstaw_wartosc(int n, int* tab, int x) {
    for (int i = 0; i < n; ++i)
        tab[i] = x;
}
```

## 4.2.2 – Operacje arytmetyczne na tablicach

```c
int suma(int n, int* tab) {
    int s = 0;
    for (int i = 0; i < n; ++i)
        s += tab[i];
    return s;
}

double srednia(int n, int* tab) {
    return (double)suma(n, tab) / n;
}

int suma_kwadratow(int n, int* tab) {
    int s = 0;
    for (int i = 0; i < n; ++i)
        s += tab[i] * tab[i];
    return s;
}
```

## 4.2.3 – Średnia arytmetyczna (tablica const)

```c
double srednia_const(int n, const int* tab) {
    int s = 0;
    for (int i = 0; i < n; ++i)
        s += tab[i];
    return (double)s / n;
}
```

## 4.2.4 – Średnia geometryczna (unsigned)

```c
#include <math.h>

double srednia_geometryczna(int n, const unsigned int* tab) {
    double iloczyn = 1.0;
    for (int i = 0; i < n; ++i)
        iloczyn *= tab[i];
    return pow(iloczyn, 1.0 / n);
}
```

## 4.2.5 – Pierwsza liczba pierwsza mniejsza niż n

```c
#include <stdbool.h>

int pierwsza_mniejsza_n(int n) {
    if (n <= 2) return -1;

    bool sito[n];
    for (int i = 0; i < n; ++i)
        sito[i] = true;
    sito[0] = sito[1] = false;

    for (int i = 2; i * i < n; ++i) {
        if (sito[i]) {
            for (int j = i * i; j < n; j += i)
                sito[j] = false;
        }
    }

    for (int i = n - 1; i >= 2; --i) {
        if (sito[i])
            return i;
    }
    return -1;
}
```
