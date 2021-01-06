
<!-- .slide: class="chapter-rev" -->
<!-- .element: data-visibility="hidden" -->
# Names

* N1: Choose Descriptive Names
* N2: Choose Names at the Appropriate Level of Abstraction
* N3: Use Standard Nomenclature Where Possible
* N4: Unambiguous Names
* N5: Use Long Names for Long Scopes
* N6: Avoid Encodings 
* N7: Names Should Describe Side-Effects 

inj-note:

Wybór dobrych nazw wymaga umiejętności opisywania i podstaw kulturowych. Trzeba się tego
nauczyć, ale nie jest to problemem techniczny, biznesowy ani organizacyjny.

---

### Naming Conventions


|Raw | camelCase | PascalCase | kebab-case | snake_case|
|:---|:---------:|:----------:|:----------:|:---------:|
|fruits in basket | fruitsInBasket | FruitsInBasket | fruits-in-basket | fruits_in_basket|
|has error | hasError | HasError| has-error | has_error |
|is visible | isVisible | IsVisible | is-visible | is_visible|

inj-note:

### Konwencje nazewnictwa

Można wyróżnić cztery główne konwencje nazewnictwa. 
camelCase, PascalCase, kebab-case, snake-case.

---

### G24: Follow Standard Conventions

>**Every team should follow a coding standard based on common industry norms. This coding**
>**standard should specify things like where to declare instance variables; how to name**
>**classes, methods, and variables; where to put braces; and so on.** 

**Everyone on the team should follow these conventions**. This means that, each team member must be mature enough, 
to realize, that it doesn’t matter where you put your braces, so long, as you all agree on where to put them.

inj-note:

### G24. Wykorzystanie standardowych konwencji

Każdy zespół powinien korzystać ze standardów kodowania bazujących na wspólnych normach
przemysłowych. Standard kodowania powinien definiować takie zagadnienia, jak miejsce deklaracji
zmiennych instancyjnych, sposób nazewnictwa klas, metod i zmiennych, miejsce umieszczenia
klamer i tak dalej.

Każdy członek zespołu powinien stosować się do tych konwencji. Oznacza to, że każdy członek zespołu
powinien być na tyle dojrzały, aby zgodzić się, że nie ma znaczenia, gdzie umieszcza się
klamry, dopóki wszyscy zgadzają się na jedno miejsce.

---

### N6: Avoid Encodings

Names should not be encoded with type or scope information. Prefixes such as **'m_', 'c', 's' or 'i'** <!-- .element: class="left-orient" -->
are useless in today’s environments.  <!-- .element: class="left-orient" -->

* Hungarian Notation (HN)

Majority of languages f.ex. Java, C# including CAPL are strongly typed, and editing environments can detect a type error long before you can run a compile. So nowadays HN and other forms of type encoding are simply handicaps.

Encodings are also a possibility that the encoding system will mislead the reader.<!-- .element: class="left-orient" -->

```java
PhoneNumber phoneString;
// name not changed when type changed!
```

inj-note:

### N6. Unikanie kodowania

* Unikanie kodowania - wspolczesnie zanieczyszcza kod

Kodowanie w nazwach typu lub informacji o zakresie powoduje zwiększenie nakładu pracy przy odszyfrowaniu.

Fortran wymuszał kodowanie przez użycie pierwszej litery nazwy na kod typu. 
W czesne wersje języka Basic pozwalały tylko na korzystanie z litery i jednej cyfry. 

Notacja węgierska (NW) pozwalała przejść na całkiem nowy poziom.
NW była uważana za bardzo ważną w API Windows C, gdy wszystko było uchwytem całkowitym,
długim wskaźnikiem lub wskaźnikiem void albo jedną z kilku odmian "string" (o różnych zastosowaniachi atrybutach). 
W tym czasie kompilator nie sprawdzał typów, więc programiści potrzebowali sposobu na ich zapamiętanie.

W dniu dzisiejszym notacja węgierska jest tylko utrudniniem.

W nowoczesnych językach mamy znacznie bogatszy system typów, a kompilator pamięta i wymusza typy. Co więcej,
istnieje trend tworzenia mniejszych klas i krótszych funkcji, aby ludzie najczęściej widzieli punkt deklaracji 
każdej używanej zmiennej.

---

### G25: Replace Magic Numbers with Named Constants

This is probably one of the oldest rules in software development. In general it is a bad
idea to have raw numbers in your code. Shall be hidden behind well-named constants.

Some constants are so easy to recognize that they don’t always need a named constant
to hide behind so long as they are used in conjunction with very self-explanatory code. 

```java
    double milesWalked = feetWalked/5280.0; // wlll known, easy to recgnize... maybe for an american
    int dailyPay = hourlyRate * 8;
    double circumference = radius * Math.PI * 2;
```

inj-note:

### G25. Zamiana magicznych liczb na stałe nazwane

W przypadku mPADa, magiczne liczby najczęściej są używane jako "exit codes" z funkcji. Uważam, że to jest zła praktyka.

Jest to prawdopodobnie jedna z najstarszych zasad programowania.Zwykle złym pomysłem jest korzystanie
z surowych liczb w kodzie. Niektóre stałe są tak proste do rozpoznania, że nie zawsze wymagają stałej 
nazwanej, o ile są połączone z bardzo dobrze opisującym się kodem 

Są też przypadki, wktórychy stosować liczby.

Czy faktycznie w powyższych przykładach potrzebujemy stałych FEET_PER_MILE, WORK_HOURS_PER_DAY
oraz TWO? Istnieją jednak wyrażenia, w których stałe są po prostu lepsze niż surowe liczby. 
Można mieć wątpliwości co do stałej WORK_HOURS_PER_DAY, ponieważ prawo i konwencje mogą się zmieniać. 
Z drugiej strony, wyrażenie to czyta się tak dobrze z cyfrą, że byłbym ostrożny przed dodawaniem do niego 17 znaków. 

W przypadku FEET_PER_MILE liczba 5280 jest tak dobrze znana i unikatowa, że czytelnik rozpozna ją, nawet gdyby znajdowała się
sama na stronie, bez żadnego kontekstu.

Stałe, takie jak 3,141592653589793, są również bardzo dobrze znane i łatwo rozpoznawalne. Jednak
szansa popełnienia błędu jest zbyt duża, aby pozostawić ją w surowej postaci. Za każdym razem,
gdy ktoś zobaczy 3,1415927535890793, będzie wiedział, że jest to pi, i nie będzie jej sprawdzał (czy
zauważyłeś błąd w jednej cyfrze?). Nie chcemy również, aby używane były wartości 3,14, 3,14159,
3,142 i tak dalej. Dlatego dobrze, że mamy już zdefiniowaną stałą Math. PI.

---

### G25: Replace Magic Numbers with Named Constants

The term “Magic Number” does not apply only to numbers. It applies to any token
that has a value that is not self-describing. 

```java
    assertEquals(7777, Employee.find(“John Doe”).employeeNumber());
```

There are two magic numbers in this assertion. The first is obviously **"7777"**. 
The second magic number is **"John Doe"**.

It also turns out that "John Doe" represents hourly paid, test employee in that test database. 
So this test should really read:

```java
    assertEquals(HOURLY_EMPLOYEE_ID, Employee.find(HOURLY_EMPLOYEE_NAME).employeeNumber());
```

inj-note:

### G25. Zamiana magicznych liczb na stałe nazwane

Termin „magiczna liczba” nie odnosi się wyłącznie do liczb. Odnosi się do dowolnej wartości, która
nie jest rozpoznawalna na pierwszy rzut oka. Na przykład:

W tej asercji mamy dwie magiczne liczby. Pierwszą jest 7777, ponieważ jej znaczenie nie jest oczywiste.
Drugą magiczną liczbą jest "John Doe", ponieważ i w tym przypadku intencje nie są jasne.
Wygląda to tak, jakby "John Doe" był nazwą pracownika numer 7777 w testowej bazie danych. 
Każdy po podłączeniu do tej bazy będzie miał dostęp do danych kilku pracowników mających znane wartości i atrybuty. 
"John Doe" reprezentuje jedynego pracownika opłacanego godzinowo w tej testowej bazie danych. 

---

### N1: Choose Descriptive Names

* Class Names

**Classes, structures and objects** should have **noun or noun phrase names** like: Customer, WikiPage,
Account, and AddressParser. A class name should not be a verb.

* Method Names

**Methods** should have **verb or verb phrase names** like: postPayment, deletePage, or save.
**Accessors, mutators, predicates** should be prefixed with '**get, set, is**'.

Choosing good names for **one argument function can go together with the arguments**. Function and argument should form a very nice verb/noun pair. 

```java
//is very evocative. Whatever this “name” thing is, it is being “written.”
write(name) 
//even better name might be below, which tells us that the “name” thing is a “field.”
writeField(name)
```

inj-note:

### N1: Wybór opisowych nazw

* Nazwy Klas

Klasy, struktury i obiekty powinny być rzeczownikami lub wyrażeniami rzeczownikowymi, takimi jak: Customer,
WikiPage, Account czy też AddressParser. Należy unikać w nazwach klas słów takich jak: Manager,
Processor, Data lub Info. Nazwy klas nie powinny być czasownikami.

* Nazwy metod

Metody należy opatrywać nazwami będącymi czasownikami lub wyrażeniami czasownikowymi,
takimi jak postPayment, de1etePage lub save. Akcesory, mutatory być poprzedzone przedrostkiem **get, set lub is**.


Funkcja i argument mogą tworzyć użyteczną parę czasownik-rzeczownik, co poprawia czytelmpść kodu. 


Na przykład zapis write (name) jest oczywisty. Niezależnie od tego, czym jest name (nazwa), jest to poddawane operacji write (zapis). Jeszcze lepszą nazwą może być write Field (name), z której jednoznacznie wynika, że zapisywana jest nazwa pola.

---
### N1: Choose Descriptive Names

Names in software are 90% of what make software readable. You need to take the time to choose them wisely and keep them relevant.

```C
public int x() {
    int q = 0;
    int z = 0;
    for (int kk = 0; kk < 10; kk++) {
        if (l[z] == 10)
        {
            q += 10 + (1[z + 1] + 1[z + 2]);
            z += 1;
        }
        else if (l[z] + l[z + 1] == 10)
        {
            q += 10 + 1 [z + 2];
            z += 2;
        } else {
            q += l[z] + l[z + 1];
            z += 2;
        }
    }
    return q
}
```

inj-note:

### N1: Wybór opisowych nazw

W 90 procentach nazwy w kodzie decydują o jego czytelności. Pamiętaj, że znaczenie nazwy, dryfuje w czasie, nie wahaj się zmieniać nazwy, którą wybrałeś. 


Nie podejmuj szybko decyzji na temat danej nazwy. Nazwa powinna być stosowna oraz isotna. 
Bądź pewien, że nazwa jest wystarczjąco opisowa.

Poniżej mamy ten sam kod zapisany we właściwy sposób. Magiczne liczby przestały być magiczne,  a struktura algorytmu jest zachęcająco opisowa.

```java
private boolean isStrikeiint frame) {
    return rolls[frame] == 10;
}
```
---

### N1: Choose Descriptive Names

- Use Intention-Revealing Names

The name of a variable, function, or class, should tell you why it exists, what it does, 
and how it is used. So take care with your names. 

```C
public int score() {
    int score = 0;
    int frame = 0;
    for (int frameNumber = 0; frameNumber < 10; frameNumber++) {
        if (isStrike(frame)) {
            score += 10 + nextTwoBallsForStrikeiframe);
            frame += 1;
        } else if (isSpareiframe)) {
            score += 10 + nextBallForSpareiframe);
            frame += 2;
        } else {
            score += twoBallsInFrame(frame);
            frame += 2;
        }
    }    
    return score;
}
```

inj-note:

### N1: Wybór opisowych nazw

To jest ten sam kod co na poprzednim slajdzie.

- Używaj nazw przedstawiających intencje/zamiary

Wybór odpowiedniej nazwy to dobra inwestycja - zajmuje trochę
czasu, ale pozwala oszczędzić go znacznie więcej. Dlatego warto przyglądać się używanym nazwom i zmieniać je, gdy znajdziemy lepsze. Każdy, kto czyta Twój kod (włącznie z Tobą), skorzysta na tym.

---

### N3: Use Standard Nomenclature Where Possible

Names are easier to understand if they are based on existing convention or usage.
In Java, for example, functions that convert objects to string representations are often named:

```java
toString();
```
Teams will often invent their own standard system of names for a particular project.
Your code should use the terms from this language extensively.

More you can use names that are overloaded with special meanings that are relevant 
to your project, the easier it will be for readers to know what your code is talking about.

inj-note:

### N3. Korzystanie ze standardowej nomenklatury tam,gdzie jest to możliwe

Nazwy są łatwiejsze do zrozumienia, jeżeli bazują na istniejących konwencjach lub zastosowaniach.
W języku Java funkcje konwertujące obiekty na postać znakową są często nazywane toString.
Lepiej zachować zgodność z tego typu konwencjami, niż wymyślać własne.

Zespoły często wymyślają własne standardy nazewnictwa dla określonych projektów.

Mówiąc krótko, im więcej używamy nazw przeładowanych znaczeniami odnoszącymi
się do naszego projektu, tym łatwiej będzie czytelnikowi zrozumieć, do czego służy dany kod.

---

### N4: Unambiguous Names

Choose names that make the workings of a function or variable unambiguous. 
Names may seem long, however it’s explanatory value outweighs the length cost.

* Avoid Disinformation  <!-- .element: class="left-orient" -->

  + Do not refer to specific phrases, unless you know it's truly represents it.
```java
// The word list means something specific to programmers.
// account list is actually a dictionary, but by the name indicates on the list
var accountList = new Dictionary<string, int>();
//  account list is truely a list
var accountList = new List<int>();
```
  + Beware of using names which vary in small ways.  <!-- .element: class="left-orient" -->
```java
// It is not ewasy to distinguish both variables
var yzControllerForEfficientHandlingOfStrings = new YZControllerForEfficientHandlingOfStrings();
var xyzControllerForEfficientStorageOfStrings = new XYZControllerForEfficientStorageOfStrings();
```

inj-note:

### N4. Jednoznaczne nazwy

Należy wybierać nazwy, które nie pozostawiają niejednoznaczności co do działania funkcji lub
zmiennej. Nazwy mogą wydawać się długie, niemniej ich wartość objaśniająca przewyższa koszt ich długości. 

- Unikanie dezinformacji

  + Unikaj używania nazw, które mogą być nazwami własnymi. Może to prowadzić do fałszywych wniosków.
  + Należy unikać nazw, które nieznacznie się od siebie różnią.

```java
// It is not ewasy to distinguish both variables
var yzControllerForEfficientHandlingOfStrings = new YZControllerForEfficientHandlingOfStrings();
var xyzControllerForEfficientStorageOfStrings = new XYZControllerForEfficientStorageOfStrings();
```
---

### N4: Unambiguous Names

Example of disinformative names would be the use of lower-case **l** or uppercase **O** as variable names, 
especially in combination. The problem is that they look almost entirely like the constants one and zero.

```C
int a = l;
if ( O == l )
    a = O1;
else
    l = 01;
```

inj-note:

### N4. Jednoznaczne nazwy

Przykładem niezwykle dezinformujących działań jest użycie w nazwach małej litery L oraz wielkiej O,
Problem oczywiście polega na tym, że litery te wyglądają niemal tak jak cyfry jeden i zero.
---

### N4: Unambiguous Names

- Use Pronounceable Names. This matters because programming is a social activity. Hungarian notation and prefixes make names unpronouceable. <!-- .element: class="left-orient" -->

```
// bad naming
int XPstn = 1;
// better naming
int xPosition = 1; 
```

- Avoid Mental Mapping.  This is a problem with single-letter variable names.  <!-- .element: class="left-orient" -->

```java
// good loop counter
customers[i];
customers[j];
customers[k];
// bad loop counter
// Seems like number '1'
customers[l];
```

inj-note:

### N4. Jednoznaczne nazwy

- Tworzenie nazw, które można wymówić

Znaczna część naszego mózgu jest stworzona do interpretacji słów. Słowa z definicji dają się wymówić. 
Jeżeli nie będziemy mogli ich wymówić, nie będzie można swobodnie dyskutować o kodzie. 
Ma to znaczenie, ponieważ programowanie jest aktywnością społeczną. Prefixy i notacja wegierska utrudniaja
wymowienie nazwy.

- Unikanie odwzorowania mentalnego

Czytający kod nie powinni mentalnie przekształcać naszych nazw na inne. 

---

### N4: Unambiguous Name

* Don’t Be Cute  <!-- .element: class="left-orient" -->

Choose clarity over entertainment value.  <!-- .element: class="left-orient" -->
```java
// bad naming
void hollyHandGranade();
// good naming
void deleteAllItems();
```

* Pick One Word per Concept
Pick one word for one abstract concept and stick with it. For instance, it’s confusing 
to have **fetch, retrieve, and get** as equivalent methods of different classes.

inj-note:

### N4. Jednoznaczne nazwy

* Nie bądź dowcipny

Jeżeli nazwy są dowcipnymi szaradami, mogą być zapamiętane wyłącznie przez osoby z identycznym
co autor poczuciem humoru, i tylko dopóty, dopóki będą one pamiętać dany żart słowny. 
Czy wszyscy będą wiedzieli, do czego służy funkcja o nazwie HolyHandGrenade?
Czytelność jest zawsze ważniejsza od wrażeń artystycznych

* Wybieraj jedno słowo na pojęcie

Należy stosować zasadę jedno słowo na jedno abstrakcyjne pojęcie i trzymać się jej. 
Na przykład mylące jest stosowanie nazw fetch, retrieve i get do analogicznych 
metod w różnych klasach.

---

### N4: Unambiguous Name

If names must be different, then they should also mean something different.  <!-- .element: class="left-orient" -->

* Make Meaningful Distinctions  <!-- .element: class="left-orient" -->

    + Number-series naming **(a1, a2, .. aN)**    
        It is the opposite of intentional naming. Such names are noninformative.
    + Noise words like **Info, Data, the, a, an, variable**
        Noise words are redundant. The word variable should never appear in a variable name.

inj-note:

### N4. Jednoznaczne nazwy

Jeżeli nazwy muszą być różne, to powinny one również znaczyć coś innego.

- Tworzenie wyraźnych różnic
  * Nazwy korzystające z numerów kolejnych (al, a2, ... aN) są przeciwieństwem nazw znaczących. Nazwy te nie są dezinformujące. Nie niosą ze sobą żadnej informacji o intencjach autora.
  * Szum słowny. Słowa **Info, Data, the,a, an, variable**, są równie mało znaczącymi nazwami. Nazwy powinny różnić się w taki sposób, aby czytelnik wiedział, na czym polega różnica. Jeżeli utworzymy inną klasę, o nazwie ProductInfo lub ProduetData, otrzymamy różne nazwy, ale nie spowodujemy, że będą one znaczyły coś innego.

---

### N5: Use Long Names

- Use Long Names for Long Scopes

The length of a name should be related to the length of the scope. You can use very short
variable names for tiny scopes, but for big scopes you should use longer names.

```python
def make_md_from_from_sfa_tokens(tokens) -> str:
    md = '' # short scope
    for token in tokens:
        local_md = make_md_description_from_sfa_token(token)
        md += local_md + '\r\n'
    return md
```

- Use Searchable Names

Single-letter names and numeric constants have a particular problem in that they are not
easy to locate across a body of text.

inj-note:

* Użycie długich nazw dla długich zakresów

Długość nazwy powinna być związana z długością zakresu. Można używać bardzo krótkich nazw
dla niewielkich zakresów, ale dla dużych zakresów powinny być używane długie nazwy.

* Korzystanie z nazw łatwych do wyszukania

Nazwy jednoliterowe i stałe numeryczne, są szczególnie niewygodne, ponieważ nie można ich łatwo
wyszukać w tekście.

Podobnie jest z nazwą **'e'** . Jest złym wyborem, jeżeli jest używana do zmiennej, którą programista będzie
chciał kiedykolwiek znaleźć. Jest to najczęściej występująca litera w języku angielskim i najprawdopodobniej
zostanie wyszukana w każdym fragmencie tekstu. Pod tym względem dłuższe nazwy przewyższają krótsze.


---
<!-- .element: data-visibility="hidden" -->
### N5: Use Long Names for Long Scopes

* Member Prefixes

You also don’t need to prefix member variables with m_ anymore. Your classes and functions
should be small enough that you don’t need them. And you should be using an editing
environment that highlights or colorizes members to make them distinct.

```java
public class Part {
    private String m_dsc; 
    void setName(String name) {
        m dsc = name;
    }
}
```

inj-note:

Nie potrzebujemy już przedrostków m_ dla zmiennych składowych. Nasze klasy i funkcje powinny
być na tyle małe, aby nie były one potrzebne. Powinniśmy używać środowiska edycyjnego, które
wyróżnia lub koloruje składniki.

```java
public class Part {
    String description;
    void setDescriptionCString description){
        this.description = description;
    }
}
```

Oprócz tego ludzie szybko uczą się ignorować przedrostki (lub przyrostki), aby widzieć znaczącą
część nazwy. Im częściej czytamy kod, tym mniej widzimy przedrostków. W końcu staną się one
nie zauważalnym szumem i znacznikiem starszego kodu.

---

<!-- .element: data-visibility="hidden" -->
### N7: Names Should Describe Side-Effects

Names should describe everything that a function, variable, or class is or does. Don’t hide
side effects with a name. 

```java
public ObjectOutputStream getOosi) throws IOException {
    if (m_oos == nuli) {
        m_oos = new ObjectOutputStreamim_socket.getOutputStreami));
    }
    return m_oos;
}
```

The hardest thing about choosing good names is that it requires good descriptive skills and
a shared cultural background. This is a teaching issue rather than a technical, business, or
management issue. As a result many people in this field don’t learn to do it very well.

inj-note:

### N7. Nazwy powinny opisywać efekty uboczne
Nazwy powinny opisywać wszystko, co wykonuje dana funkcja, zmienna lub klasa. Nie należy
ukrywać efektów ubocznych w nazwie. Nie należy używać prostego słowa do opisania funkcji, która
wykonuje więcej niż tylko tę prostą akcję.

---

<!-- .element: data-visibility="hidden" -->
### G19: Use Explanatory Variables

One of the more powerful ways to make a program readable is to break the calculations 
up into intermediate values that are held in variables with meaningful names.

``` java
Matcher match = headerPattern.matcher(line);
if(match.find())
{
    String key = match.group(1);
    String value = match.group(2);
    headers.put(key.toLowerCase(), value);
}
```

The simple use of explanatory variables makes it clear that the first matched group is
the key, and the second matched group is the value. More explanatory variables are 
generally better than fewer. 

inj-note:

### G19. Użycie opisowych zmiennych

Jednym z najefektywniejszych sposobów zapewnienia czytelności programu jest 
podzielenie obliczeń na kroki pośrednie, których wyniki są przechowywane 
w zmiennych o znaczących nazwach.

Dzięki użyciu zmiennych opisowych od razu wiadomo, że pierwsza znaleziona grupa jest kluczem,
a druga wartością.
Trudno zrobić to lepiej. Im więcej zmiennych opisowych, tym lepiej. Trudno uwierzyć, jak szybko
nieczytelny moduł staje się przejrzysty, gdy tylko podzielimy obliczenia na dobrze nazwane wartości
pośrednie.

---

<!-- .element: data-visibility="hidden" -->

### G11: Inconsistency

If you do something a certain way, do all similar things in the same way. This goes back
to the principle of least surprise. 

Be careful with the conventions you choose, and once chosen, be careful to continue to follow them.
If within a particular function you use a variable named response to hold an
HttpServletResponse, then use the same variable name consistently in the other functions
that use HttpServletResponse objects. 

If you name a method processVerificationRequest,then use a similar name, such as processDeletionRequest,
 for the methods that process other kinds of requests.
Simple consistency like this, when reliably applied, can make code much easier to
read and modify.

inj-note:

### G11 . Niespójność

Jeżeli wykonujemy coś w określony sposób, wszystkie podobne zadania powinniśmy wykonywać
w taki sam sposób. Odnosi się to do zasady najmniejszego zaskoczenia. Należy rozważnie wybierać
konwencje i po ich wybraniu konsekwentnie je stosować.
Jeżeli w określonej funkcji korzystamy ze zmiennej o nazwie response, zawierającej HttpServlet
-►Response, to tej samej nazwy zmiennej powinniśmy używać we wszystkich innych funkcjach korzystających
z obiektu Http5ervletResponse. Jeżeli nazwiemy metodę processVerificationRequest,
to powinniśmy użyć podobnej nazwy, takiej jak processDeletionRequest, dla metod przetwarzających
inne rodzaje żądań.
Tego typu prosta spójność, jeżeli jest konsekwentnie stosowana, może spowodować, że kod będzie
znacznie łatwiejszy do czytania i modyfikacji.

---

### Code excercises

<iframe  width=600 height=140 class="ace stretch">// Not clear namig
class DtaRcrd102 {
  private Date genymdhms;
  private Date modymdhms;
  private final String pszqint = "102";

};
// More clear intensions
class Customer {
  private Date generationTimestamp;
  private Date modificationTimestamp;;
  private final String recordId = "102";

};
</iframe>

inj-note:

---

### Code excercises

<iframe  width=600 height=140 class="ace stretch">// Variables with unclear context.
private void printGuessStatistics(char candidate, int count) {
  
  String number;
  String verb;
  String pluralModifier;

  if (count == 0) {
    number = "no";
    verb = "are";
    pluralModifier = "s";
  } else if (count == 1) {
    number = "1";
    verb = "is";
    pluralModifier = "";
  } else {
    number = Integer.toString(count);
    verb = "are";
    pluralModifier = "s";
  }

  String guessMessage = String.format(
    "There %s %s %s%s", verb, number, candidate, pluralModifier
  );

  print(guessMessage);
}

// Variables have a context

public class GuessStatisticsMessage {

  private String number;
  private String verb;
  private String pluralModifier;

  public String make(char candidate, int count) {
    createPluralDependentMessageParts(count);
    return String.format(
      "There %s %s %s%s",
      verb, number, candidate, pluralModifier );
  }
  private void createPluralDependentMessageParts(int count) {
    if (count == 0) {
      thereAreNoLetters();
    } else if (count == 1) {
      thereIsOneLetter();
    } else {
      thereAreManyLetters(count);
    }
  }

  private void thereAreManyLetters(int count) {
    number = Integer.toString(count);
    verb = "are";
    pluralModifier = "s";
  }

  private void thereIsOneLetter() {
    number = "1";
    verb = "is";
    pluralModifier = "";
  }

  private void thereAreNoLetters() {
    number = "no";
    verb = "are";
    pluralModifier = "s";
  }
}
</iframe>

inj-note:
