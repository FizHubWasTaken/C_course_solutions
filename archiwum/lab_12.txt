#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <time.h>

#define N 5


/*
---------------------------------------------
Zad. 1.
---------------------------------------------
*/
void przypisz(double (*p_arr)[N], time_t ziarno){
    srand(ziarno);

    for(int i = 0; i < N; i++){
        for(int j = 0; j < N; j++){
            p_arr[i][j] = (double)rand() / RAND_MAX;
        }
    } 
}


/*
---------------------------------------------
Zad. 2.
---------------------------------------------
*/
void wypisz(double arr[N][N]){
    for(int i = 0; i < N; i++){
        for(int j = 0; j < N; j++){
            printf("%lf ", arr[i][j]);
        }
        printf("\n");
    }
    printf("\n");
}


/*
---------------------------------------------
Zad. 3.
---------------------------------------------
*/
int transponuj(double arr[N][N]){
    double t;
    int jest_symetryczna = 1;

    for (int i = 0; i < N; i++){
        for (int j = 0; j < i; j++) {
            double t = arr[i][j];
            arr[i][j] = arr[j][i];
            arr[j][i] = t;

            if(!(arr[i][j] == arr[j][i])){
                jest_symetryczna = 0;
            }
        }
    }

    return jest_symetryczna;
}


/*
---------------------------------------------
Zad. 4.
---------------------------------------------
*/
double trace(double* element){
    double trace = 0;
    for(int i = 0; i < N; i++){
        trace += *(element + i * (N + 1));
    }
    return trace;
}


/*
---------------------------------------------
Zad. 5.
---------------------------------------------
*/
void wypisz_dane(char** znaki){
    for(int i = 0; i < 2; i++){
        for(int j = 0; j < strlen(znaki[i]); j++){
            printf("%c", znaki[i][j]);
        }
        printf("\n");
    }

    // puts() drukuje łańcuch znaków, więc:
    //
    // for(int i = 0; i < 2; i++){
    //     puts(znaki[i]);
    // }   
}


int main(void){
    // 1.
    double arr[N][N];
    przypisz(&arr[0], time(0));

    // 2.
    wypisz(arr);

    // 3.
    int symetryczna = transponuj(arr);
    wypisz(arr);

    if(symetryczna) printf("Macierz jest symetryczna\n");
    else printf("Macierz nie jest ortogonalna\n\n");

    // 4.
    printf("Ślad macierzy wynosi: %lf\n\n", trace(&arr[0][0]));


    // 5.
    char* dane[2] = {"Barack", "Obama"};
    wypisz_dane(&dane[0]);
}