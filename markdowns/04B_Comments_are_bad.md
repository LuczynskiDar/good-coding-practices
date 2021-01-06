
<!-- .slide: class="chapter-rev" -->
<!-- .element: data-visibility="hidden" -->
# Bad Comments 

* <a href="#/inapropriate-info"> C1: Inappropriate Information </a>
* C2: Obsolete Comment
* C3: Redundant Comment 
* C4: Poorly Written Comment
* C5: Commented-Out Code 

inj-note:

They are not “pure good.” Indeed, comments are, at best, a necessary evil.

The proper use of comments is to compensate for our failure to express ourself in
code. Note that I used the word failure. I meant it. Comments are always failures. We must
have them because we cannot always figure out how to express ourselves without them,
but their use is not a cause for celebration.

Why am I so down on comments? Because they lie. Not always, and not intentionally,
but too often. The older a comment is, and the farther away it is from the code it describes,
the more likely it is to be just plain wrong. The reason is simple. Programmers can’t realistically
maintain them.

inj-note:

Nie są one "czystym dobrem". W rzeczywistości komentarze są w najlepszym przypadku koniecznym złem. 
Prawidłowe zastosowanie komentarzy jest kompensowaniem naszych błędów przy tworzeniu kodu (wysławianiu się w kodzie).
Obecność komentarzy zawsze sygnalizuje nieporadność programisty. Musimy korzystać z nich, ponieważ nie zawsze wiemy,
jak wyrazić nasze intencje bez ich użycia, ale ich obecność nie jest powodem do świętowania.

Gdy uznamy, że konieczne jest napisanie komentarza, należy pomyśleć, czy nie istnieje sposób na
wyrażenie tego samego w kodzie. 
Dlaczego jestem tak przeciwny komentarzom? Ponieważ one kłamią. Nie zawsze, nie rozmyślnie,
ale nader często. Im starsze są komentarze, tym większe prawdopodobieństwo, że są po prostu
błędne. Powód jest prosty. Programiści nie są w stanie utrzymywać ich aktualności.

---

### C3: Redundant Comment

A comment is redundant if it describes something that adequately describes itself. 
Comments should say things that the code cannot say for itself.

```C
i++; // increment i
```

inj-note:

### C3. Nadmiarowe komentarze
Komentarz jest nadmiarowy, jeżeli opisuje coś, co wystarczająco dobrze samo się opisuje. Komentarze powinny informować o tym, o czym nie może powiedzieć sam kod.

---

### C3: Redundant Comment

* Journal Comments

Sometimes people add a comment to the start of a module every time they edit it. These comments accumulate as a kind of journal, or log, of every change that has ever been made. Nowadays, we have source code control systems, these long journals make harder to read the code.

```java
  /*
    * Changes (from 11-Oct-2001)
    * --------------------------
    * 11-Oct-2001 : Re-organised the class and moved it to new package
    * com.jrefinery.date (DG);
    * 05-Nov-2001 : Added a getDescription() method, and eliminated NotableDate
    * class (DG);
    * 12-Nov-2001 : IBD requires setDescription() method, now that NotableDate
    * class is gone (DG); Changed getPreviousDayOfWeek(),
    * getFollowingDayOfWeek() and getNearestDayOfWeek() to correct
    * bugs (DG);
    * 05-Dec-2001 : Fixed bug in SpreadsheetDate class (DG);
    * 29-May-2002 : Moved the month constants into a separate interface
    * (MonthConstants) (DG);
    * 27-Aug-2002 : Fixed bug in addMonths() method, thanks to Nlevka Petr (DG);
    * 03-Oct-2002 : Fixed errors reported by Checkstyle (DG);
    * 13-Mar-2003 : Implemented Serializable (DG);
    * 29-May-2003 : Fixed bug in addMonths method (DG);
    * 04-Sep-2003 : Implemented Comparable. Updated the isInRange javadocs (DG);
    * 05-Jan-2005 : Fixed bug in addYears() method (1096282) (DG);
 */
```
<!-- .element: class="stretch" -->

inj-note:

### C3. Nadmiarowe komentarze

* Komentarze dziennika

Czasami programiści dodają na początku każdego pliku komentarz informujący o każdej edycji. Komentarze takie tworzą pewnego rodzaju dziennik wszystkich wprowadzonych zmian. 

Dawno temu istniały powody tworzenia i utrzymywania takich dzienników na początku każdego
modułu. Nie mieliśmy po prostu systemów kontroli wersji, które wykonywały to za nas. Obecnie
jednak takie długie dzienniki tylko pogarszają czytelność modułu. Powinny zostać usunięte

---

<!-- .element: data-visibility="hidden" -->
### C1: Inappropriate Information

* Misleading Comments

Sometimes, with all the best intentions, a programmer makes a statement in his comments
that isn’t precise enough to be accurate. Consider for another moment the badly redundant
but also subtly misleading comment 

This subtle bit of misinformation, couched in a comment that is harder to read than
the body of the code, could cause another programmer to blithely call this function in the
expectation that it will return as soon as this.closed becomes true. That poor programmer
would then find himself in a debugging session trying to figure out why his code executed
so slowly.

inj-note:

It is inappropriate for a comment to hold information better held in a different kind of system
such as your source code control system, your issue tracking system, or any other
record-keeping system. Change histories, for example, just clutter up source files with
volumes of historical and uninteresting text. In general, meta-data such as authors, lastmodified-
date, SPR number, and so on should not appear in comments. Comments should
be reserved for technical notes about the code and design.

* Mylące komentarze
Czasami pomimo najlepszych intencji programista zapisuje w komentarzu nieprecyzyjne zdania.
Wróćmy na moment do nadmiarowego, ale również nieco mylącego komentarza zamieszczonego
na listingu 4.1.

```java
\\Metoda użytkowa kończąca pracę, gdy this.closed ma wartość true. Zgłasza wyjątek,
\\ jeżeli przekroczony zostanie czas oczekiwania.
public synchronized void waitForClose(final long timeoutMillis)
throws Exception
if ( ! closed)
{
wait(timeoutMillis) ;
if ( ! closed)
    throw new Exception("MockResponseSender could not be closed");

```
Czy Czytelnik zauważył, w czym ten komentarz jest mylący? Metoda ta nie kończy się, gdy
this. closed ma wartość true. Kończy się ona, jeżeli this. closed ma wartość true; w przeciwnym
razie czeka określony czas, a następnie zgłasza wyjątek, jeżeli this. closed nadal nie ma
wartości true.
Ta subtelna dezinformacja umieszczona w komentarzu, który czyta się trudniej niż sam kod, może
spowodować, że inny programista naiwnie wywoła tę funkcję, oczekując, że zakończy się od razu,
gdy this. closed przyjmie wartość true. Ten biedny programista może zorientować się, o co
chodzi, dopiero w sesji debugera, gdy będzie próbował zorientować się, dlaczego jego kod działa
tak powoli.

---

### C3: Redundant Comment

* Noise Comments

Sometimes you see comments that are nothing but noise. They restate the obvious and provide no new information.
```java 
/**
* Default constructor.
*/
protected AnnualDateRule() {
}

/** The day of the month. */
private int dayOfMonth;

/**
* Returns the day of the month.
*
* @return the day of the month.
*/
//Give me a break!
public int getDayOfMonth() {
return dayOfMonth;
}

```
<!-- .element: class="stretch" -->

These comments are so noisy that we learn to ignore them, our eyes tend to skip them over. <!-- .element: class="left-orient" -->

inj-note:

### C3. Nadmiarowe komentarze

* Komentarze wprowadzające szum informacyjny

Czasami zdarza się nam spotkać komentarze, które nie są niczym więcej jak tylko szumem informacyjnym.

Dzien miesiaca, getter dnia miesiaca, nie wnoszą nic nowego oprócz szumu, a zczasem nasze oczy bedą się uczyły je ignorować.

Przedstawiają one oczywiste dane i nie dostarczają żadnych nowych informacji.

---

### C3: Redundant Comment

* Don’t Use a Comment When You Can Use a Function or a Variable

Consider the following stretch of code:<!-- .element: class="left-orient" -->

```java
    // does the module from the global list <mod> depend on the
    // subsystem we are part of
    if (smodule
            .getDependSubsystems()
            .contains(subSysMod.getSubSystem())
        ){}
```
This could be rephrased without the comment as:<!-- .element: class="left-orient" -->
```java
    ArrayList moduleDependees = smodule.getDependSubsystems();
    String ourSubSystem = subSysMod.getSubSystem();
    if (moduleDependees
            .contains(ourSubSystem)
        ){}
```
Sometimes cleanerCode != smarterCode <!-- .element: class="left-orient" -->

inj-note:

### C3. Nadmiarowe komentarze

* Nie używaj komentarzy, jeżeli można użyć funkcji lub zmiennej

Autor prawdopodobnie napisał komentarz na początku (niestety), a następnie
kod realizujący zadanie z komentarza. Jeżeli jednak autor zmodyfikowałby kod w sposób, w jaki ja
to wykonałem, komentarz mógłby zostać usunięty.

---

### C3: Redundant Comment 

* Position Markers

Sometimes programmers like to mark a particular position in a source file. <!-- .element: class="left-orient" -->

```java
// Actions //////////////////////////////////
```

Right after eliminating long tail of slashes, sometimes it makes sense to use such marker to gather certain functions together. But in general they are clutter that should be eliminated. 
Use them occasionally, and only when the benefit is significant. If too many, our eyes learn to ignore them.

inj-note:

### C3. Nadmiarowe komentarze

* Znaczniki pozycji

Czasami programiści lubią zaznaczać określone miejsca w pliku źródłowym.

```java
// Akcje //////////////////////////////////
```

Zaraz po wyeliminowaniu tego ogona slashy, czsem ma sen stosowanie tego typu markerów
jeżeli chcemy zgromadzić okreslone funkcje razem. Niemniej najeczęściej tego typu
znaczniki tworzą bałagan, który powinien być wyelimonowany. Tak więc warto używać ich oszczędnie i tylko wtedy, gdy ich zalety są wyraźne. Jeżeli zbyt często używamy tych
transparentów, zaczynają być traktowane jako szum tła i ignorowane.

---

### C3: Redundant Comment 

* Closing Brace Comments

Although this might make sense for long functions with deeply nested structures, it serves only to clutter the kind of small and encapsulated functions that we prefer. So if you find yourself wanting to mark your closing braces, try to shorten your functions instead.

```java
while ((line = in.readLine()) != null) {
    lineCount++;
    charCount += line.length();
    String words[] = line.split("\\W");
    wordCount += words.length;
} //while
```

inj-note:

### C3. Nadmiarowe komentarze

* Komentarze w klamrach zamykających

Komentaże w klamrach zamykających mogą mieć sens w przypadku długich funkcji, z głęboko zagnieżdżonymi strukturami, w małych i hermetycznych funkcjach, jakie preferujemy, tworzą tylko nieład. Jeżeli więc chcesz mieć klamry zamykające, lepiej zamiast tego skrócić funkcję.
Ja nie polecam stosowania takich kontarzy. Ostanim razem widzialem to na studiach i nigdzie indziej.

---

### C3: Redundant Comment 

* Attributions and Bylines

```java
/* Added by Rick */
```

Source code control systems are very good at remembering who added what, when. There is no need to pollute the code with little bylines. 

inj-note:

### C3. Nadmiarowe komentarze

* Atrybuty i dopiski

Systemy kontroli wersji świetnie nadają się do zapamiętywania, kto (i kiedy) dodał określony
fragment. Nie ma potrzeby zaśmiecania kodu tymi małymi dopiskami. Można uważać, że tego typu
komentarze będą przydatne do sprawdzenia, z kim można porozmawiać na temat danego fragmentu
kodu. Rzeczywistość jest inna - zwykle zostają tam przez lata, tracąc na dokładności i użyteczności.
Pamiętajmy - systemy kontroli wersji są lepszym miejscem dla tego rodzaju informacji

---

### C3: Redundant Comment

* Too Much Information

The comment below was extracted from a module designed to test that a function could encode and decode base64 coding. 

It is good enough to have RFC number, someone reading this code has no need for the arcane information contained in the comment.
```java
/*
RFC 2045 - Multipurpose Internet Mail Extensions (MIME)
Part One: Format of Internet Message Bodies
section 6.8. Base64 Content-Transfer-Encoding
The encoding process represents 24-bit groups of input bits as output
strings of 4 encoded characters. Proceeding from left to right, a
24-bit input group is formed by concatenating 3 8-bit input groups.
These 24 bits are then treated as 4 concatenated 6-bit groups, each
of which is translated into a single digit in the base64 alphabet.
When encoding a bit stream via the base64 encoding, the bit stream
must be presumed to be ordered with the most-significant-bit first.
That is, the first bit in the stream will be the high-order bit in
the first 8-bit byte, and the eighth bit will be the low-order bit in
the first 8-bit byte, and so on.
*/
```
<!-- .element: width="50%" height="auto" class="stretch"  -->

inj-note:

### C3. Nadmiarowe komentarze

* Nadmiar informacji

Nie należy umieszczać w komentarzach interesujących z punktu widzenia historii dyskusji lub luźnych opisów szczegółów. 
Komentarz zamieszczony poniżej został pobrany z modułu mającego za
zadanie sprawdzić, czy funkcja może kodować i dekodować zgodnie ze standardem base64. 
Osoba czytająca ten kod numer referencyjny do standardu RFC powinien być wystarczający, tam jest pełna informacja na temat standardu kodowania base64, stąd komentarz jest zbędny.

---

### C3: Redundant Comment

* Mandated Comments

It is just plain silly to have a rule that says that every function must have a doc, or every variable must have a comment. Comments like this just clutter up the code, propagate lies.
```java
/**
*
* @param title The title of the CD
* @param author The author of the CD
* @param tracks The number of tracks on the CD
* @param durationInMinutes The duration of the CD in minutes
*/
public void addCD(String title, String author, int tracks, int durationInMinutes) {
    CD cd = new CD();
    cd.title = title;
    cd.author = author;
    cd.tracks = tracks;
    cd.duration = duration;
    cdList.add(cd);
}
```

inj-note:

### C3. Nadmiarowe komentarze

* Komentarze wymagane

Wymaganie, aby każda funkcja posiadała Javadoc lub aby każda zmienna posiadała komentarz, jest po prostu głupie. Tego typu komentarze tylko zaciemniają kod i prowadzą do powszechnych
pomyłek i dezorganizacji.

Takie komentarze nie wnoszą niczego, za to utrudniają zrozumienie
kodu.

---
<!-- .element: data-visibility="hidden" -->
### C1: Inappropriate Information

* Nonlocal Information

Make sure the comment describes the code thar appears near. Don’t offer systemwide information in the context of a local comment. The function has absolutely no control over what that default is. The comment is not describing the function, but some other, far distant part of the system. 

```java
/**
* Port on which fitnesse would run. Defaults to <b>8082</b>.
*
* @param fitnessePort
*/
public void setFitnessePort(int fitnessePort)
{
    this.fitnessePort = fitnessePort;
}
```

inj-note:

### C1: Inappropriate Information

* Informacje nielokalne

Jeżeli konieczne jest napisanie komentarza, to należy upewnić się, że opisuje on kod znajdujący się
w pobliżu. Nie należy udostępniać informacji dotyczących całego systemu w kontekście komentarzy
lokalnych. Weźmy jako przykład zamieszczone poniżej komentarze Javadoc. Pomijając fakt, że
są zupełnie zbędne, zawierają one informacje o domyślnym porcie. Funkcja jednak nie ma absolutnie
żadnej kontroli nad tą wartością domyślną. Komentarz nie opisuje funkcji, ale inną część
systemu, znacznie od niej oddaloną. Oczywiście, nie ma gwarancji, że komentarz ten zostanie
zmieniony, gdy kod zawierający wartość domyślną ulegnie zmianie.


---

<!-- .element: data-visibility="hidden" -->
### C4: Poorly Written Comment

* Mumbling 

If you decide to write a comment, then spend the time necessary to make sure it is the best comment you can write.
```java
// Utility method that returns when this.closed is true. Throws an exception
// if the timeout is reached.
public synchronized void waitForClose(final long timeoutMillis) throws Exception
{
    if(!closed)
    {
        wait(timeoutMillis);
        if(!closed)
        throw new Exception("MockResponseSender could not be closed");
    }
}

public void loadProperties()
{
    try
    {
        String propertiesPath = propertiesLocation + "/" + PROPERTIES_FILE;
        FileInputStream propertiesStream = new FileInputStream(propertiesPath);
        loadedProperties.load(propertiesStream);
    }
    catch(IOException e)
    {
       // No properties files means all defaults are loaded
    }
}
```
inj-note:

prosta funkcja z komentarzem w nagłówku, który jest całkowicie
zbędny. Prawdopodobnie dłużej zajmuje przeczytanie komentarza niż samego kodu
Simple function with a header comment that is completely redundant. The comment probably takes longer to read than the code itself.
A comment worth writing is worth writing well. If you are going to write a comment,
take the time to make sure it is the best comment you can write. Choose your words
carefully. Use correct grammar and punctuation. Don’t ramble. Don’t state the obvious.

* Bełkot

Pisanie komentarza tylko dlatego, że czujemy, iż powinien być napisany lub też że wymaga tego proces, jest błędem. Jeżeli decydujemy się na napisanie komentarza, musimy poświęcić nieco czasu na upewnienie się, że jest to najlepszy komentarz, jaki mogliśmy napisać.

Co oznacza komentarz w bloku c a t c h? Jasne jest, że znaczy on coś dla autora, ale znaczenie to nie
zostało dobrze wyartykułowane. Jeżeli otrzymamy wyjątek IOException, najwyraźniej oznacza to
brak pliku właściwości.

Być może - ta możliwość jest nieco przerażająca - autor próbował powiedzieć sobie, że powinien wrócić w to miejsce i napisać kod ładujący wartości domyślne.

Jedynym sposobem, aby się tego dowiedzieć, jest przeanalizowanie kodu z innych części systemu
i sprawdzenie, co się w nich dzieje. 
Wszystkie komentarze, które wymuszają zaglądanie do innych
modułów w celu ich zrozumienia, nie są warte bitów, które zajmują.

---

### C4: Poorly Written Comment

* Inobvious Connection

The connection between a comment and the code it describes should be obvious. If you are
going to the trouble to write a comment, then at least you’d like the reader to be able to look at the comment and the code and understand what the comment is talking about. 

```java
/*
* start with an array that is big enough to hold all the pixels
* (plus filter bytes), and an extra 200 bytes for header info
*/
this.pngBytes = new byte[((this.width + 1) * this.height * 3) + 200];
```
What is filter, what is its the relation to '**+ 1**' or '*** 3**' or both of them? Is the pixel a '**byte**'? Why header info takes '**200 bytes**'?

inj-note:

### C4: Poorly Written Comment

* Nieoczywiste połączenia

Połączenie pomiędzy komentarzem a kodem, który on opisuje, powinno być oczywiste. Jeżeli mamy problemy z napisaniem komentarza, to powinniśmy przynajmniej doprowadzić do tego, by czytelnik
patrzący na komentarz i kod rozumiał, o czym mówi dany komentarz.

Zadaniem komentarza jest wyjaśnianie kodu, który sam się nie objaśnia. Szkoda, że sam komentarz wymaga dodatkowego objaśnienia.

---

### C5: Commented-Out Code 

* Commented-Out Code

Don’t do this! Others who see that commented-out code won’t have the courage to delete it. They’ll think it is there for a reason and is too important to delete. That code sits there and rots, getting less and less relevant with every passing day. It calls functions that no longer exist. It uses variables whose names have changed.<!-- .element: class="left-orient" -->

```java
InputStreamResponse response = new InputStreamResponse();
response.setBody(formatter.getResultStream(), formatter.getByteCount());
// InputStream resultsStream = formatter.getResultStream();
// StreamReader reader = new StreamReader(resultsStream);
// response.setContent(reader.read(formatter.getByteCount()));
```

Source code control systems will remember the code for us. We don’t have to comment it out any more. Just delete the code. 

inj-note:

Niewiele jest praktyk tak nieprofesjonalnych, jak zakomentowanie kodu. Nie rób tego!

Inni programiści, którzy zobaczą taki zakomentowany kod, nie będą mieli odwagi go usunąć. Uznają, że jest tam z jakiegoś powodu i że jest zbyt ważny, aby go usunąć. W ten sposób zakomentowany kod zaczyna się odkładać jak osad na dnie butelki zepsutego wina.

Jednak od bardzo długiego czasu mamy już dobre systemy kontroli wersji. Systemy te pamiętają za nas wcześniejszy kod. Nie musimy już komentować kodu. Po prostu możemy go usunąć

---
<!-- .element: data-visibility="hidden" -->
### C2: Obsolete Comment

A comment that has gotten old, irrelevant, and incorrect is obsolete. Comments get old
quickly. It is best not to write a comment that will become obsolete. If you find an obsolete
comment, it is best to update it or get rid of it as quickly as possible. Obsolete comments
tend to migrate away from the code they once described. They become floating islands of
irrelevance and misdirection in the code.

inj-note:

### C2. Przestarzałe komentarze

Komentarz, który stał się nieistotny i nieprawidłowy, jest przestarzały. Komentarze bardzo szybko
się starzeją. Najlepiej nie pisać komentarzy, które mogą utracić aktualność. Jeżeli znajdziemy przestarzały
komentarz, najlepiej jak najszybciej go zaktualizować lub usunąć. Przestarzałe komentarze
mają tendencję do utraty łączności z opisywanym kodem. Stają się one pływającymi wyspami
nieistotności i błędnymi kierunkowskazami w kodzie.

---

### Code excercises

<iframe  width=600 height=140 class="ace stretch">// Commented-out lines of code
/* No longer used as has been replaced by DoSomethinElse().
public void DoSomething()
{
    // ...implementation...
}
*/
</iframe>

inj-note:
