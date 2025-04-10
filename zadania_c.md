
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

# Implementacje zadań 4.2.6 – 4.2.19 w języku C

## Zadanie 4.2.6
```c
void zad4_2_6a(int n, int tab1[], int tab2[]) {
    for (int i = 0; i < n; i++) tab2[i] = tab1[i];
}

void zad4_2_6b(int n, int tab1[], int tab2[]) {
    for (int i = 0; i < n; i++) tab2[n - 1 - i] = tab1[i];
}
```

## Zadanie 4.2.7
```c
void zad4_2_7a(int n, int tab1[], int tab2[], int tab3[]) {
    for (int i = 0; i < n; i++) tab3[i] = tab1[i] + tab2[i];
}

void zad4_2_7b(int n, int tab1[], int tab2[], int tab3[]) {
    for (int i = 0; i < n; i++) tab3[i] = (tab1[i] > tab2[i]) ? tab1[i] : tab2[i];
}

void zad4_2_7c(int n, int tab1[], int tab2[], int tab3[]) {
    for (int i = 0; i < n; i++) {
        tab2[i] = tab1[i];
        tab3[i] = tab2[i];
        tab1[i] = tab3[i];
    }
}
```

## Zadanie 4.2.8
```c
void zad4_2_8a(int n, int tab1[], int tab2[], double tab3[]) {
    for (int i = 0; i < n; i++) tab3[i] = tab1[i] + tab2[i];
}

void zad4_2_8b(int n, int tab1[], int tab2[], double tab3[]) {
    for (int i = 0; i < n; i++) {
        tab3[2 * i] = tab1[i];
        tab3[2 * i + 1] = tab2[i];
    }
}
```

## Zadanie 4.2.9
```c
void zad4_2_9(int n, int tab1[], int tab2[], int tab3[]) {
    for (int i = 0; i < n; i++) {
        int max = tab1[i];
        if (tab2[i] > max) max = tab2[i];
        if (tab3[i] > max) max = tab3[i];
        tab1[i] = max;

        int a = tab1[i], b = tab2[i], c = tab3[i];
        int first = a > b ? (a > c ? a : c) : (b > c ? b : c);
        int second = (a + b + c) - first - (a < b ? (a < c ? a : c) : (b < c ? b : c));
        tab2[i] = second;

        int min = tab1[i];
        if (tab2[i] < min) min = tab2[i];
        if (tab3[i] < min) min = tab3[i];
        tab3[i] = min;
    }
}
```

## Zadanie 4.2.10
```c
int zad4_2_10(int n, int tab[], char typ) {
    int max = tab[0], min = tab[0], index_max = 0, index_min = 0;
    for (int i = 1; i < n; i++) {
        if (tab[i] > max) { max = tab[i]; index_max = i; }
        if (tab[i] < min) { min = tab[i]; index_min = i; }
    }
    switch (typ) {
        case 'a': return max;
        case 'b': return min;
        case 'c': return index_min;
        case 'd': return index_max;
        case 'e': return max - min;
        default: return -1;
    }
}
```

## Zadanie 4.2.11
```c
double zad4_2_11(int n, double tab[]) {
    double iloczyn = 1.0;
    for (int i = 0; i < n; i++) iloczyn *= tab[i];
    return iloczyn;
}
```

## Zadanie 4.2.12
```c
void zad4_2_12a(int n, int tab[]) {
    int last = tab[n - 1];
    for (int i = n - 1; i > 0; i--) tab[i] = tab[i - 1];
    tab[0] = last;
}

void zad4_2_12b(int n, int tab[]) {
    int first = tab[0];
    for (int i = 0; i < n - 1; i++) tab[i] = tab[i + 1];
    tab[n - 1] = first;
}

void zad4_2_12c(int n, int tab[]) {
    for (int i = 0; i < n / 2; i++) {
        int temp = tab[i];
        tab[i] = tab[n - 1 - i];
        tab[n - 1 - i] = temp;
    }
}

void zad4_2_12d(int n, int tab[]) {
    for (int i = 0; i < n - 1; i++) {
        for (int j = 0; j < n - i - 1; j++) {
            if (tab[j] > tab[j + 1]) {
                int temp = tab[j];
                tab[j] = tab[j + 1];
                tab[j + 1] = temp;
            }
        }
    }
}
```

## Zadania 4.2.13 – 4.2.19
```c
int* zad4_2_13(int n) {
    int* tab = (int*)malloc(n * sizeof(int));
    return tab;
}

double* zad4_2_14(int n) {
    double* tab = (double*)malloc(n * sizeof(double));
    return tab;
}

void zad4_2_15(int* tab) {
    free(tab);
}

void zad4_2_16(double* tab) {
    free(tab);
}

double* zad4_2_17(int n, double tab[]) {
    double* nowa = (double*)malloc(n * sizeof(double));
    for (int i = 0; i < n; i++) nowa[i] = tab[i];
    return nowa;
}

int* zad4_2_18(int n, int tab1[], int tab2[]) {
    int* suma = (int*)malloc(n * sizeof(int));
    for (int i = 0; i < n; i++) suma[i] = tab1[i] + tab2[i];
    return suma;
}

int* zad4_2_19(int n, int tab1[], int* liczba_niezerowych) {
    int* tab2 = (int*)malloc(n * sizeof(int));
    int licznik = 0;
    for (int i = 0; i < n; i++) {
        if (tab1[i] != 0) tab2[licznik++] = tab1[i];
    }
    *liczba_niezerowych = licznik;
    return tab2;
}
```

