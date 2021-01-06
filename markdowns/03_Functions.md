
<!-- .slide: class="chapter-rev" -->
<!-- .element: data-visibility="hidden" -->
# Functions

* G20: Function Names Should Say What They Do
* G30: Functions Should Do One Thing  
* F1: Too Many Arguments
* F2: Output Arguments 
* F3: Flag Arguments 
* F4: Dead Function 

---
### G30: Functions Should Do One Thing 

> **Single responsibility rule** 
> * FUNCTIONS SHOULD DO ONE THING
> * THEY SHOULD DO IT WELL
> * THEY SHOULD DO IT ONLY

* Sections within Functions

```java
// Bad example, fuction pay() does 3 operations
public void pay() {
    for (Employee e : employees) { // review data of each emploee
        if (e.isPayday()) { // checks if emploee is allowd to pay
            Money pay = e.calculatePay(); // then finally calculates the paymen and pays
            e.deliverPay(pay);
        }
    }
}
```

inj-note:

### Funkcje powinny robić tylko jedną rzecz 

* Sekcje wewnąrz funkcji

Ten fragment kodu wykonuje trzy operacje. Przegląda dane pracowników, sprawdza, czy kolejnemu
pracownikowi należy zapłacić, a następnie realizuje wypłatę.

Funkcje które mają wiele sekcji wykonujących serię działań powinny zostać zamienione na mniejsze.

---

### G30: Functions Should Do One Thing 

Functions that do one thing cannot be reasonably divided into sections.  <!-- .element: class="left-orient" -->


```java
// Better example
public void pay() {
    for (Employee e : employees){
        paylfNecessary(e);
    }
}
private void payIfNecessary(Employee e) {
    if (e.isPaydayi)){
        calculateAndDeliverPay(e);
    }   
}
private void calculateAndDeliverPay(Employee e) {
    Money pay = e .calculatePayi);
    e.deliverPay(pay);
}

```

### Small Functions

Functions should not be 100 lines long. Functions should hardly ever be 20 lines long. <!-- .element: class="left-orient" -->

inj-note:

Funkcje, które robia tylko jedną rzecz nie mogą być podzielone na sekcje.

Pierwsza zasada dotycząca konstruowania funkcji jest taka, że powinny być małe.

Funkcje nie powinny mieć 100 wierszy długości. Funkcje powinny mieć nie więcej niż 20 wierszy.

---

### G20: Function Names Should Say What They Do

Would you expect this to add five days to the date? Or is it weeks, or hours?
You can’t tell from the call what the function does.
```java
// bad example
// Does it add 5 days, weeks or hours to the date?
Date newDate = date.add(5);
```
If the function adds five days to the date and changes the date:<!-- .element: class="left-orient" -->
```java
//better solution, if it incraeses by 5 days the better solution coold be
date.increaseByDays(5);
```

inj-note:

Czy funkcja spowoduje dodanie pięciu dni do daty? Czy też tygodni lub godzin?
Nie jesteśmy w stanie stwierdzić, co robi funkcja.

Jeżeli musimy spojrzeć do implementacji (lub dokumentacji) funkcji w celu sprawdzenia, co ona robi, to powinniśmy zmienić jej nazwę na lepszą lub zmienić jej implementację.

---

### G5: Duplication

This is one of the most important rules in this book, it's been called DRY principle (Don’t Repeat Yourself). 

> OO itself is a strategy for organizing modules and eliminating duplication.  
> **Find** and **eliminate duplication** wherever you can.

More subtle duplications are the modules that have similar algorithms, but that don’t share
similar lines of code.

inj-note:

### G5. Powtórzenia

Jest to jedna z najważniejszych książki Czysty Kod. Nazwają 
ją też zasadą DRY (ang. Don’t Repeat Yourself), czyli „nie powtarzaj się”.

Powtarzanie to jest problemem, ponieważ powoduje rozdęcie kodu, wymaga więcej modyfikacji,
w przypadku zmian algorytmu oraz zwiększa możliwość popełnienia błędu.

Samo programowanie obiektowe jest strategią organizacji modułów i eliminowania powtórzeń. 

Bardziej subtelnym rodzajem powtórzeń są moduły, które mają podobne algorytmy, ale nie mają podobnego kodu.

---

### F1: Too Many Arguments

**No argument is best**, followed by one, two, and three. More than three is very questionable and should be avoided. They take a lot of conceptual power. **Arguments are even harder from a testing point of view**, because demands to write many test cases to ensure that all the various combinations of arguments work properly. If there are no arguments, this is trivial.

When a function seems to need more than two or three arguments, it is likely that some of those arguments ought to be **wrapped into a class of their own**.

```java
    Circle makeCircle(double x, double y, double radius);
    Circle makeCircle(Point center, double radius);
```
Reducing the number of arguments by creating objects out of them may seem like cheating, but it’s not. When groups of variables are passed together, they are likely part of a concept.
inj-note:

### F1. Nadmiar argumentów

Funkcje powinny mieć małą liczbę argumentów. Najlepszym przypadkiem jest... brak argumentów,
następnie mogą być: jeden, dwa lub trzy argumenty. Większa liczba argumentów stanowi potencjalne
źródło problemów. Argumenty są kłopotliwe. Wymagają one użycia sporej ilości
energii koncepcyjnej. 

Argumenty są jeszcze bardziej kłopotliwe z punktu widzenia testowania. Trudno napisać wszystkie
testy jednostkowe zapewniające, że wszystkie kombinacje argumentów będą działały prawidłowo.
Jeżeli nie ma argumentów, jest to bardzo proste.

Gdy wydaje się, że funkcja wymaga więcej niż dwóch lub trzech argumentów, najprawdopodobniej
niektóre z nich powinny być umieszczone w osobnej klasie. 

Zmniejszenie liczby argumentów przez utworzenie z nich obiektów może wydawać się oszustwem,
ale tak nie jest. Gdy grupy zmiennych są przesyłane wspólnie, tak jak x oraz y w powyższym przykładzie,
najprawdopodobniej są częścią obiektu, który zasługuje na własną nazwę.

---

### G10: Vertical Separation

+ **Variables and function** should be defined close to where they are used. Local variables
should be declared just above their first usage and should have a small vertical scope.

+ **Dependent functions** should be defined just below their first usage. If one function calls another, 
they should be vertically close, and the caller should be above the callee. This gives the program a naturalflow. 

inj-note:

### G10. Separacja pionowa

* Zmienne i funkcje powinny być definiowane blisko miejsca, gdzie są użyte. Zmienne lokalne powinny
być deklarowane bezpośrednio ponad pierwszym użyciem i powinny mieć mały zakres pionowy.
Nie chcemy zmiennych lokalnych deklarowanych setki wierszy od ich zastosowania.

* Funkcje zależne. Jeżeli jedna funkcja wywołuje inną, powinny być one położone blisko siebie, a funkcja
wywołująca powinna być umieszczona powyżej wywoływanej, o ile jest to możliwe. Pozwala to
osiągnąć naturalny przebieg programu. Jeżeli konwencja ta jest stosowana konsekwentnie, czytelnik
będzie mógł zaufać nam, że definicja funkcji znajduje się zaraz po jej wywołaniu. 

---

### G10: Vertical Separation

* Reading Code from Top to Bottom: The Stepdown Rule

The code should be read like a top-down, every function to be followed by those at the next 
level of abstraction so that we can read the program, descending one level of abstraction 
at a time as we read down the list of functions. I call this The Stepdown Rule.

inj-note:

### Czytanie kodu od góry do dołu - zasada zstępująca

Chcemy, aby kod można było czytać od góry do dołu. Chcemy, aby po każdej funkcji znajdowała
się kolejna, na następnym poziomie abstrakcji, dzięki czemu można czytać program, schodząc
o jeden poziom abstrakcji niżej wraz z przejściem do kolejnej funkcji w pliku. Nazywam to zasadą
zstępującą.

Inaczej mówiąc, chcemy, aby można było czytać program tak, jakby był zbiorem akapitów,
z których każdy opisuje bieżący poziom abstrakcji odwołujących się do kolejnych akapitówna następnym poziomie.

Praktyka pokazuje, że programiści mają problemy z przyswojeniem sobie tej reguły i pisaniem
funkcji działających na jednym poziomie abstrakcji. Programista, który chce być profesjonalistą,
powinien jednak wypracować sobie nawyk tworzenia krótkich funkcji, które na pewno wykonują
"jedną operację". 

---

<!-- .element: data-visibility="hidden" -->

### F3: Flag Arguments

Boolean arguments indicate that the function does more than one thing. It does one thing if the flag is true and another if the flag is false!

inj-note:

### F3. Argumenty znacznikowe

Argumenty logiczne deklarują, że funkcja wykonuje więcej niż iedną operację. Są one mylące
i powinny być eliminowane. Argumenty znacznikowe są brzydkie. Przekazanie wartości boolean 
do funkcji jest naprawdę niepraktyczne. Od razu komplikuje to sygnaturę metody, wyraźnie 
informując, że funkcja wykonuje więcej niż jedną operację. Wykonuje jedną operację, 
jeżeli znacznik ma wartość true, i inną, jeżeli znacznik ma wartość false.

---

### F4: Dead Function / G9: Dead Code

**Dead code is code that isn’t executed.** The problem with dead code is that after awhile it starts to smell. 
This is because dead code is not completely updated when designs change. 

It still compiles, but it does not follow newer conventions or rules. It was written at a time when the system was different. 
When you find **dead code, delete it from the system**. Do not afraid, your source code control system still remembers it.

inj-note:

### F4. Martwe funkcje / Martwy kod

Martwy kod to taki, który nie jest wykonywany. Problem z martwym kodem jest taki, że szybko zaczyna 
wydzielać zapach. Im jest starszy, tym ten zapach staje się silniejszy i kwaśniejszy. 
Dzieje się tak, ponieważ martwy kod nie jest w pełni aktualizowany w czasie zmian projektu. 

Nadal kompiluje się, ale nie jest zgodny z najnowszymi konwencjami i zasadami. 
Był on pisany w czasie, gdy system był inny. 

Gdy znajdziemy martwy kod, możemy zrobić tylko jedną właściwą rzecz, usunąć go.
Nie trzeba się obawiać usuwania funkcji — system kontroli wersji nadal ją pamięta.

---

### G29: Avoid Negative Conditionals
Negatives are harder to understand than positives. So, when possible, conditionals
should be expressed as positives. 
```java
// Is worse, negative conditional
if (!buffer.shouldNotCompact())
// Is better, positive conditional
if (buffer.shouldCompact())

```

inj-note:

### G29. Unikanie warunków negatywnych

Warunki negatywne są nieco trudniejsze do zrozumienia niż pozytywne. Dlatego, jeżeli jest to
możliwe, wyrażenia powinny być formułowane jako warunki pozytywne.

---

### G35: Keep Configurable Data at High Levels

**Constant** such as a **default or configuration value** that is known and expected
at a high level of abstraction, **do not bury it in a low-level function**. 
Expose it as an argument to that low-level function called from the high-level function. 

inj-note:

Jeżeli mamy stałe, takie jak wartości domyślne lub konfiguracyjne, które są oczekiwane na wysokim
poziomie abstrakcji, to nie należy ukrywać ich w funkcjach niskiego poziomu. Należy ujawnić je
jako argumenty, z użyciem których funkcje niskiego poziomu są wywoływane z funkcji wysokiego
poziomu.

Stałe konfiguracji znajdują się na bardzo wysokim poziomie i łatwo je zmienić. Są one przekazywane
w dół, do pozostałych części aplikacji.
