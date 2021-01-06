
### Blocks and Indenting

```java
public class FitNesseServer implements SocketServer { private FitNesseContext
context; public FitNesseServerCFitNesseContext context) { this.context =
context; } public void serveCSocket s) { serveCs, 10000); } public void
serveCSocket s, long requestTimeout) { try { FitNesseExpediter sender = new
FitNesseExpediterCs, context); sender.setRequestParsingTimeLimitCrequestTimeout); sender.startC); }
catchCException e) { e.printStackTraceC); } } }
```
* Code formatting is about communication   <!-- .element: class="left-orient" -->

A source file is a hierarchy rather like an outline. To make this hierarchy of scopes visible, 
we indent the lines of source code in proportion to their position in the hiearchy. 
This allows them to quickly hop over scopes. Without indentation, programs would be virtually unreadable by humans.
However it is good enough css/js code for the minification!

* **The indent level of a function** should **not be greater than one or two**, which makes the functions easier to read and understand.

inj-note:

### Bloki  i Wcięcia

Plik źródłowy stanowi pewnego rodzaju hierarchię, a nie szablon. Znajdują się w nim informacje
odnoszące się do pliku jako całości, do poszczególnych klas w pliku, do metod w klasach, do bloków
w metodach oraz, rekurencyjnie, do bloków w blokach. Każdy poziom hierarchii jest zakresem,
w którym są zadeklarowane nazwy oraz w którym są interpretowane deklaracje i instrukcje
wykonywalne.
Aby hierarchia ta była widoczna, wcinamy wiersze kodu źródłowego odpowiednio do pozycji
w hierarchii.

---

### Vertical Formatting

Comparing 7 different projects, files that are typically ~40 lines long, with an upper limit of ~500. 
Small files are usually easier to understand than large files are. Desirable is building an app having 
from 200 to 500 lines per file, however, this should not be a hard rule.

![vertical_box_plot][vertical_box_plot] <!-- .element: width="70%" height="auto" class="stretch" -->

[vertical_box_plot]: ../markdowns/Images/05_Formatting/05.Lines_per_file.png "File length distributions" 

Figure: File length distributions LOG scale (box height = sigma)

inj-note:

EKS. I. Rozkład wielkości plików w skali logarytmicznej (wysokość prostokąta = sigma)

Porównując ze sobą pliki siedmiu projektów - Junit, FitNesse, testNG, Time and Money, JDepend,
Ant oraz Tomcat, okazuje się, żeśrednia znajduje się w pomiędzy ~40 a ~500 linii. 

Linie przechodzące przez prostokąty pokazują minimalną i maksymalną wielkość
pliku w każdym projekcie. Prostokąt pokazuje średnio jedną trzecią (jedno standardowe odchyleniel)
liczby plików. Środek prostokąta oznacza średnią.

Wydaje się, że możliwe jest zbudowanie znaczącego systemu plików mających przeciętnie 200 wierszy, 
a nieprzekraczających 500 wierszy. Choć nie musi to być sztywna reguła, to jednak powinna być bardzo 
pożądana. Małe pliki są zwykle łatwiejsze do zrozumienia niż duże.

---

### Vertical Openness Between Concepts

Nearly all code is read left to right and top to bottom. Each line represents an expression or
a clause, and each group of lines represents a complete thought. Those thoughts should be
separated from each other with blank lines.

```python
def is_str_instance(v):
    return isinstance(v, str)


def hex_str_to_int(input: str) -> int:
    return int(input, 16)


def int_to_hex(input: int) -> hex:
    return hex(int)
```

inj-note:

### Pionowe odstępy pomiędzy segmentami kodu

Przykladem PEP 8 w python, nakazuje 2 linie odstepu miedzy definicjami funkcji,
natomiast w ciele klasy metody, czy zmienne maja jedną linię odstępu. 

Niemal każdy kod czyta się od lewej do prawej i od góry do dołu. Każdy wiersz reprezentuje wyrażenie
lub klauzulę, a każda grupa wierszy reprezentuje kompletną myśL Myśli te powinny być oddzielone
od siebie pustymi wierszami.

---

<!-- .element: data-visibility="hidden" -->

### Vertical Ordering

This is the exact opposite of languages like Pascal, C, and C++ that enforce functions to be defined, 
or at least declared, before they are used.

In general we want function call dependencies to point in the downward direction. That is, a function that is called should be below a function that does the calling. This creates a nice flow down the source code module from high level to low level.


inj-note:

Funkcje zależne. Jeżeli jedna funkcja wywołuje inną, powinny być one położone blisko siebie, a funkcja
wywołująca powinna być umieszczona powyżej wywoływanej, o ile jest to możliwe. Pozwala to
osiągnąć naturalny przebieg programu. Jeżeli konwencja ta jest stosowana konsekwentnie, czytelnik
będzie mógł zaufać nam, że definicja funkcji znajduje się zaraz po jej wywołaniu.

### Uporządkowanie pionowe

Zwykle chcemy, aby w funkcji wywołania zależności były kierowane w dół. Inaczej mówiąc, wywoływana
funkcja powinna znajdować się poniżej funkcji wywołującej. Daje to efekt przepływu
sterowania w dół kodu źródłowego modułu, od wysokiego poziomu do niskiego.

W artykule prasowym oczekujemy, że najważniejsze informacje znajdą się na początku, a następnie
zostaną opisane z najmniejszą liczbą przeszkadzających detali. Oczekujemy, że najdrobniejsze
szczegóły będą przedstawione na końcu. Podobnie w przypadku kodu - pozwala to nam zapoznać
się z plikami źródłowymi i uzyskiwać ich obraz na podstawie kilku pierwszych funkcji, bez zagłębiania
się w szczegóły.

---

### Horizontal Formatting

Below figure suggests that we should strive to keep lines short. The old Hollerith limit was 80, currently lines edging out to 100 or even 120 are fine. Beyond that is probably just careless. But monitors are too wide for that nowadays, and programmers can shrink the font so small that they can get 200 characters across the screen. Don’t do that.

![line_width][line_width] <!-- .element: width="65%" height="auto" class="stretch"  -->

[line_width]: ../markdowns/Images/05_Formatting/06.Line_width_distribution.png "Line width distribution" 

Figure. Java line width distribution

inj-note:

Przedstawiony jest rozkład długości wierszy wszystkich siedmiu projektów. Wiersze krótsze niż
10 znaków stanowią 30% całej populacji, natomiast wiersze o średniej długości od 20 do 60
znaków stanowią 40% całej populacji, co daje już w sumie 70%. Linie z ilością znaków do 120
zdecydowanie przekraczają 80% całej populacji (zasada pareto).
Programiści preferują krótkie wiersze. A zatem powinniśmy tworzyć krótkie wiersze. 
Stare ograniczenie Holleritha do 80 znaków jest zbyt restrykcyjne i osobiście nie 
mam nic przeciwko wierszom mającym 100, a nawet 120 znaków. Jednak wartości powyżej tej granicy są zbyt duże.

Obecnie monitory są bardzo szerokie, a młodsi programiści mogą tak zmniejszyć czcionkę, że uzyskują
wiersze o długości 200 znaków. Nie jest to dobra praktyka. Ja staram się nie przekraczać długości
120 znaków.

---

### Horizontal Openness and Density

We use horizontal white space to associate things that are strongly related and disassociate
things that are more weakly related.

``` java
private void measureLine(String line) {
    lineCount++;
    int lineSize = line.length();
    totalChars += lineSize;
    lineWidthHistogram.addLine(lineSize, lineCount);
    recordWidestLine(lineSize);
}
```
* Spaces between assignment operators
* No spaces between function name and opening parenthesis

inj-note:

### Poziome odstępy i gęstość

Odstępy poziome służą do kojarzenia elementów ściśle powiązanych i rozłączania elementów, które
są ze sobą luźniej związane. 

Operatory przypisania otoczyłem odstępami w celu ich wyróżnienia. Instrukcje przypisania mają
dwa osobne główne elementy: lewą i prawą stronę. Odstępy powodują, że rozdzielenie to jest
oczywiste.
Z drugiej strony, nie dodaję odstępów pomiędzy nazwami funkcji a otwierającymi nawiasami.
Funkcje i argumenty są ze sobą bardzo ściśle związane. Rozdzielenie ich spowodowałoby, że wyglądałyby
na rozłączone, a nie złączone. Rozdzielam argumenty wywołania funkcji, aby zaznaczyć
przecinek i pokazać, że argumenty są osobne.

---

### Horizontal Alignment

Horizontal alignment was common for assembly language programmers. That this kind of alignment is not useful. 
The alignment seems to emphasize the wrong things and leads my eye away from the true intent. You are tempted 
to read down the list of variable names without looking at their types.
```java
public class FitNesseExpediter implements ResponseSender
{
    private   Socket          socket;
    private   InputStream     input;
    private   OutputStream    output;
    private   Request         request;
    private   Response        response;
    private   FitNesseContext context;
    protected long            requestParsingTimeLimit;
    private   long            requestProgress;
    private   long            requestParsingDeadline;
    private   boolean         hasError;
    public    FitNesseExpediter(Socket          s, 
                                FitNesseContext context) throws Exception
    {
        this.context =            context;
        socket =                  s;
        input =                   s.getInputStream();
        output =                  s.getOutputStream();
        requestParsingTimeLimit = 10000;
    }
}
```
<!-- .element: class="stretch" -->

Automatic reformatting tools usually eliminate this kind of alignment.<!-- .element: class="left-orient" -->

inj-note:

### Rozmieszczenie poziome

Programując w asemblerze, stosowało się rozmieszczenie poziome w celu wyróżniania
określonych struktur. 

Niemniej tego typu wyrównywanie nie jest użyteczne. Wyrównanie takie powoduje skupienie uwagi 
na niewłaściwych elementach i odciąga wzrok od właściwych. Na przykład w przedstawionej powyżej 
liście deklaracji mamy pokusę czytania listy zmiennych bez zwracania uwagi na ich typy. 
Podobnie w instrukcjach przypisania zwykle patrzymy na listę wartości, bez zwracania uwagi 
na operator przypisania. Co gorsza, automatyczne narzędzia formatujące zwykle eliminują 
tego rodzaju wyrównanie.

---

### Code excercises

<iframe  width=600 height=140 class="ace stretch">//Improper indentation

public void DoSomething()
{
for (var i = 0; i < 1000; i++)
{
var productCode = $"PRC000{i}";
//...implementation
}

</iframe>

inj-note:
