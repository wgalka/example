# AiSD

## Problem Plecakowy
|        i|0 |1 |2 |3 |4 | 
|---------|--|--|--|--|--|
|Objetość |6 |2 |3 |2 |3 |
|Wartość  |6 |4 |5 |7 |10|

Poszukujemy kombinacji przedmiotów które umieszczając w plecaku będą mały najwiekszą wartość. 

Pojemność plecaka jest równa 23.

Znając pojemność plecaka i objętość najmniejszego przedmiotu możemy policzyć maksymalną ilość przedmiotów w plecaku.

$$
23/2 = 11
$$

Nasza przestrzeń poszukiwania to wszystkie kombinacje z powtórzeniami n cyfrowe gdzie n jest od 1 do 11. (każdy kolejny rząd znacznie zwiększa ilość stanów do przeszukania)
```terminal
[0]
[1]
[2]
[0, 0]
[1, 0]
[2, 0]
[0, 1]
[1, 1]
[2, 1]
[0, 2]
[1, 2]
[2, 2]
...

```

### Task 1
Wygenerować wszystkie kombinacje z powtórzeniami n liczbowe.

Prosty przykład generowania kombinacji z powtórzeniami liczb 3 cyfrowych:
```java
public class Task1 {
    public static void main(String[] args) {

        int[] elems = {0,1,2,3,4};
        for (int elem1: elems){
            for (int elem2: elems){
                for(int elem3:elems){
                    System.out.println("["+elem1+", "+elem2+", "+elem3+"]");
                }
            }
        }
    }
}
```

```terminal
[0, 0, 0]
[0, 0, 1]
[0, 0, 2]
[0, 0, 3]
[0, 0, 4]
[0, 1, 0]
[0, 1, 1]
[0, 1, 2]
[0, 1, 3]
...
[4, 3, 4]
[4, 4, 0]
[4, 4, 1]
[4, 4, 2]
[4, 4, 3]
[4, 4, 4]
```

### Task 2
Jak widać w poprzednim przykładzie generowanie kombinacji wykonać można przez wywołanie zagnieżdzonych pętli for. Teraz trzeba znaleźć sposób na generowanie n pętli for wewnątrz. Można to osiągnąć np za pomocą rekurencji.

```java
import java.util.Arrays;

public class Main {
    static int[] comb; //w tej zmiennej będą przechowywane kombinacje

    public static void main(String args[]) {


        int[] x={0,1,2,3,4};// tutaj przechowuję zbior liczb z ktorych będą tworzone kombinację - w naszym przypadku indeksy tablicy

        comb = new int[3+1]; // Utworzenie tablicy do przechowywania kombinacji.
        gen(x,3); //Wywołanie funkcji która będzie wypisywać 3 elementowe kombinacje ze zbioru x
    }

    public static void gen(int[] elems, int glebokoscdrzewa){
        if(glebokoscdrzewa<0){//jeśli zmienimy indeks zerowy znaczy ze jesteśmy w liściu i mamy finalną kombinację
            System.out.print(Arrays.toString(comb)+"\n");
            return;}
        for(int elem:elems){// dla kazdego elementu w tablicy elems funkcja się rozgałęzia
            comb[glebokoscdrzewa]=elem;//zmieniamy element na itej pozycji
            gen(elems,glebokoscdrzewa-1); // Wywołujemy kolejne rozgałęzienie
        }
    }
}

```


### Task 3
Mając sposób na genetowanie n elementowych kombinacji modyfikujemy kod tak aby wypisywał kombinacje n elementowe od 0 do 11 elementów.

```java
import java.util.Arrays;

public class Main {
    static int[] comb; //w tej zmiennej będą przechowywane kombinacje

    public static void main(String args[]) {


        int[] x={0,1,2,3,4};// tutaj przechowuję zbior liczb z ktorych będą tworzone kombinację - w naszym przypadku indeksy tablicy


        for(int glebokosc=0;glebokosc<11;glebokosc++){//musimy przetestować kombinacje od 1 do 10 elementów. będziemy wywoływać metodę gen z roznymi paramtrami iter
            comb = new int[glebokosc+1];
            gen(x,glebokosc);
        }
    }

    public static void gen(int[] elems, int glebokoscdrzewa){
        if(glebokoscdrzewa<0){//jeśli zmienimy indeks zerowy znaczy ze jesteśmy w liściu i mamy finalną kombinację
            System.out.print(Arrays.toString(comb)+"\n");
            return;}
        for(int elem:elems){// dla kazdego elementu w tablicy elems funkcja się rozgałęzia
            comb[glebokoscdrzewa]=elem;//zmieniamy element na itej pozycji
            gen(elems,glebokoscdrzewa-1); // Wywołujemy kolejne rozgałęzienie
        }
    }
}
```


### Task 4
Dodać dane na temat pojemności plecaka, objętości i wartości przedmiotów.

```java
import java.util.Arrays;

public class Main {
    static int[] comb; //w tej zmiennej będą przechowywane kombinacje

    final static int[][] przedmioty = { {6, 2, 3, 2, 3}, // objetości
                                       {6, 4, 5, 7, 10} };//wartości
    final static int pojPlecak = 23;

    public static void main(String args[]) {


        int[] x = {0, 1, 2, 3, 4};// tutaj przechowuję zbior liczb z ktorych będą tworzone kombinację - w naszym przypadku indeksy tablicy


        for (int glebokosc = 0; glebokosc < 11; glebokosc++) {//musimy przetestować kombinacje od 1 do 10 elementów. będziemy wywoływać metodę gen z roznymi paramtrami iter
            comb = new int[glebokosc + 1];
            gen(x, glebokosc);
        }
    }

    public static void gen(int[] elems, int glebokoscdrzewa) {
        if (glebokoscdrzewa < 0) {//jeśli zmienimy indeks zerowy znaczy ze jesteśmy w liściu i mamy finalną kombinację
            System.out.print(Arrays.toString(comb) + "\n");
            return;
        }
        for (int elem : elems) {// dla kazdego elementu w tablicy elems funkcja się rozgałęzia
            comb[glebokoscdrzewa] = elem;//zmieniamy element na itej pozycji
            gen(elems, glebokoscdrzewa - 1); // Wywołujemy kolejne rozgałęzienie
        }
    }
}
```

### Task 5
Dodać warunki poszukujące optymalnego rozwiązania.

```java
import java.util.Arrays;

public class Main {
    static int[] comb; //w tej zmiennej będą przechowywane kombinacje

    final static int[][] przedmioty = { {6, 2, 3, 2, 3}, // objetości
                                       {6, 4, 5, 7, 10} };//wartości
    final static int pojPlecak = 23;

    static int[] ostatecznePrzedmioty;
    static int  ostatecznaWartosc;

    public static void main(String args[]) {


        int[] x = {0, 1, 2, 3, 4};// tutaj przechowuję zbior liczb z ktorych będą tworzone kombinację - w naszym przypadku indeksy tablicy


        for (int glebokosc = 0; glebokosc < 11; glebokosc++) {//musimy przetestować kombinacje od 1 do 10 elementów. będziemy wywoływać metodę gen z roznymi paramtrami iter
            comb = new int[glebokosc + 1];
            gen(x, glebokosc);
        }

        // Wypisz rozwiązanie
        System.out.println("Najlepsza kombinacja przedmiotów to: "+Arrays.toString(ostatecznePrzedmioty));
        System.out.println("Ich wartość wynosi"+ostatecznaWartosc);
    }

    public static void gen(int[] elems, int glebokoscdrzewa) {
        if (glebokoscdrzewa < 0) {//jeśli zmienimy indeks zerowy znaczy ze jesteśmy w liściu i mamy finalną kombinację

            // Obliczamy objętość i wartość wybranych przedmiotów.
            int obj = 0;
            int wart = 0;

            for (int przedmiot: comb){
                obj+=przedmioty[0][przedmiot];
                wart+=przedmioty[1][przedmiot];
            }
            // Jeśli przedmioty mieszczą się i ich wartość jest większa niż poprzednia to zapisz wynik.
            if (obj <= 23 & wart > ostatecznaWartosc){
                //System.out.println(Arrays.toString(comb) + " "+wart + " "+ obj);
                ostatecznaWartosc = wart;
                ostatecznePrzedmioty = comb.clone(); // Musimy użyć clone ponieważ inaczej ostateczne przedmioty będą referencją do comb
            }
            return;
        }
        for (int elem : elems) {// dla kazdego elementu w tablicy elems funkcja się rozgałęzia
            comb[glebokoscdrzewa] = elem;//zmieniamy element na itej pozycji
            gen(elems, glebokoscdrzewa - 1); // Wywołujemy kolejne rozgałęzienie
        }
    }
}
```

## Problem wydawania reszty