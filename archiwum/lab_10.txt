#include <math.h>
#include <stdio.h>
#define SIZE 5


/*
---------------------------------------------
Zad. 1. trójkąty

Zmienne area i circumference są tego samego typu,
więc mogłyby być zwracane przez nadanie wartości
tab[0] i tab[1] gdzie tab to tablica przekazana
funkci, ale wtedy nie byłoby oczywiste która z
wartości to pole, a która to obwód.

Funcja compute_triangle zwraca 1,
dla trójki dłygości odcinków z których można
zbudować trójkąt, a 0 kiedy nie można.

W drugim przypadku zmienne area i circumference
dostają wartości -1, na wypadek gdyby ktoś próbował
ich użyć, pomimo tego, że funcja zwróciła 0.
---------------------------------------------
*/
int compute_triangle(double a, double b, double c, double* area, double* circumference){
    if(a + b >= c  && a + c >= b && b + c >= a){
        *circumference = a + b + c;
        double p = *circumference / 2;
        *area = p * (p - a) * (p - b) * (p - c);
        return 1;
    }
    else{
        *circumference = -1;
        *area = -1;
        return 0;
    }
}


/*
---------------------------------------------
Zad. 2. trójki

print_pythagorean_triples() sprawdza tylko trójki
gdzie a <= b <= c, więc nie wypisuje 
trójek równoważnych co do permutacji.

Dla a, b, c > 0, a*a + b*b = c*c:
c*c będzie zawsze 
    1) większe od a*a 
    2) większe od b*b,
więc print_pythagorean_triples() nie pomija
żadnej trójki pitagorejskiej.
---------------------------------------------
*/
int is_pythagorean(int a, int b, int c){
    return a*a + b*b == c*c;
}

void print_pythagorean_triples(int start, int end){
    int found_pythagorean = 0;

    printf("Trójki pitagorejskie z przedziału <%d, %d>: \n", 
            start, end);
    for(int i = start; i < end - 2; i++){
        for(int j = i; j < end - 1; j++){
            for(int k = j; k < end; k++){
                if(is_pythagorean(i, j, k)){
                    printf("%2d,  %2d,  %2d\n", i, j, k);
                    found_pythagorean = 1;
                }
            }
        }
    }

    if(!found_pythagorean) 
        printf("Nie znaleziono żadnej trójki.\n");
}


/*
---------------------------------------------
Zad. 3. odrwacanie
---------------------------------------------
*/
void reverse_array(int* p_first_element, int length){
    int* lower = p_first_element;
    int* upper = lower + length - 1;

    for(; lower < upper; lower++, upper--){
        int temp = *lower;
        *lower = *upper;
        *upper = temp;
    }
}


//zastosowanie funkcji:
int main(void){
    // 1. trójkąty
    double a = 2, b = 2, c = 3;
    double area, circumference;
    if(compute_triangle(a, b, c, &area, &circumference)){
        printf("Boki trójkąta: %.1lf, %.1lf, %.1lf.\n", a, b, c);
        printf("Pole: %.3lf\nObwód: %.3lf\n", area, circumference);
    }
    else printf("Z odcinków o długośćiach: %.1lf, %.1lf, %.1lf nie da się zbudować trójkąta.\n", a, b, c);
    printf("\n");

    
    // 2. trójki
    print_pythagorean_triples(1, 31);
    printf("\n");


    // 3. odwracanie
    int test_array[SIZE] = {000, 111, 222, 333, 444};
    for(int i = 0; i < SIZE; i++){
        printf("%03d ", test_array[i]);
    }
    printf("\n");

    reverse_array(&test_array[0], SIZE);
    for(int i = 0; i < SIZE; i++){
        printf("%03d ", test_array[i]);
    }
    printf("\n\n");
}