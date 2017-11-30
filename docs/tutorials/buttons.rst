Przyciski
-------

Jak dotychczas utworzyliśmy kod umożliwiający urządzeniu robienie czegoś.
Nazywa się to *wyjście*. Musimy też jednak umożliwić urządzeniu reagowanie.
To, na co ono reaguje nazywamy *wejściem*.

Łatwo zapamiętać: wyjście dotyczy wszystkiego co wychodzi z urządzenia,
natomiast wejście to wszystko co przychodzi do urządzenia w celu
przetworzenia.

Najłatwiejszą metodą dostarczenia *wejścia* są dwa przyciski, oznaczone
``A`` i ``B``. Musimy jakoś zmusić MicroPython do reagowania na ich
naciśnięcie.

Jest to niezwykle proste:

    from microbit import *

    sleep(10000)
    display.scroll(str(button_a.get_presses()))

Ten skrypt śpi przez 10 000 milisekund (czyli 10 sekund), a po tym
czasie na wyświetlaczu przewinie się liczba wciśnięć przycisku ``A``.
To wszystko.

Chociaż ten skrypt jest bezużyteczny, to jednak pokazuje nam kilka ciekawych
koncepcji:

#. *Funkcja* ``sleep`` usypia microbit na pewną liczbę milisekund. Jeżeli
   chcesz zatrzymać program, możesz to zrobić używając tej funkcji.
   *Funkcja* jest podobna do *metody* ale nie jest przyporządkowana do
   *obiektu* za pomocą kropki.

#. Obiekt ``button_a`` pozwala ci pobrać liczbę naciśnięć przycisku za pomocą
   *metody* ``get_presses``.

*Metoda* ``get_presses`` daje nam tylko liczbę, a ``display.scroll`` przyjmuje
tylko ciągi znaków. Dlatego musimy zmienić liczbę na ciąg znaków, co możemy
zrobić za pomocą funkcji ``str`` (skrót od angielskiego słowa
"string"), która przetwarza wszystko na ciąg znaków.

Trzeci wiersz jest jak cebula. Jeżeli przyjmiesz nawiasy za warstwy cebuli, to
zauważysz, że ``display.scroll`` zawiera ``str``, który zawiera
``button_a.get_presses``. Python próbuje rozpracować najbardziej wewnętrzne
wyrażenia najpierw, zanim przejdzie do następnej warstwy. To nazywa się
*zagnieżdżenie* - programistyczny odpowiednik rosyjskiej matrioszki.

.. image:: matrioshka.jpg

Przyjmijmy, że nacisnąłeś przycisk 10 razy. Python w następujący sposób
analizuje co się dzieje w trzeciej linii:

Python widzi pełną linię i dostaje wartość ``get_presses``::

    display.scroll(str(button_a.get_presses()))

Teraz, gdy Python wie już ile razy został wciśnięty przycisk, skonwertuje
wartość liczbową na ciąg znaków::

    display.scroll(str(10))

W końcu Python wie, co ma wyświetlić na ekranie::

    display.scroll("10")

Może ci się wydawać, że to jest mnóstwo pracy, ale MicroPython robi to
niezwykle szybko.

Pętle zdarzeń
+++++++++++

Często chcesz aby program poczekał na jakieś zdarzenie. Żeby to uzyskać, musisz
zamknąć w pętli kawałek kodu definiujący jak reagować na oczekiwane zdarzenia,
takie jak naciśnięcie przycisku.

Pętle w Pythonie tworzymy przy użyciu polecania ``while`` (ang. dopóki). Sprawdza ono czy
coś jest ``True`` (ang. prawdziwe). Jeżeli tak jest, to uruchamia *blok kodu* zwany *ciałem*
pętli. Jeżeli jednak nie jest, to przerywa wykonywanie pętli (ignorując ciało pętli)
i przechodzi do dalszej części kodu.

W Pythonie definiowanie bloków kodu jest proste. Powiedzmy, że mam listę rzeczy do
zrobienia napisaną na kartce papieru. Może to wyglądać tak::

    Zakupy
    Napraw uszkodzoną rynnę
    Skoś trawnik

Gdybym chciał nieco rozbić moją listę rzeczy do zrobienia, to mógłbym napisać
coś takiego::

    Zakupy:
        Jaja
        Boczek
        Pomidory
    Napraw uszkodzoną rynnę:
        Pożycz drabinę od sąsiada
        Znajdź młotek i gwoździe
        Zwróć drabinę
    Skoś trawnik:
        Sprawdź trawnik wokół sadzawki dla żab
        Sprawdź poziom paliwa w kosiarce

Oczywiście główne zadania są podzielone na podrzędne zadania, umieszczone
poniżej głównego zadania, z którym są powiązane i *wcięte*.
Tak więc ``Jaja``, ``Boczek`` i ``Pomidory`` są na pierwszy rzut oka
związane z zadaniem ``Zakupy``. Wcięcia ułatwiają nam sprawdzanie w jaki sposób
zadania są powiązane ze sobą.

Nazywamy to *zagnieżdżeniem*. Zagnieżdżania używamy do definiowania bloków kodu
w ten oto sposób::

    from microbit import *

    while running_time() < 10000:
        display.show(Image.ASLEEP)

    display.show(Image.SURPRISED)

Funkcja ``running_time`` zwraca liczbę milisekund od startu urządzenia.

Linia ``while running_time() < 10000:`` sprawdza czy czas pracy urządzenia
jest mniejszy od 10 000 milisekund (czyli 10 sekund). Jeżeli tak, *i tu widzimy
działanie zagnieżdżania*, to zostanie wyświetlony
``Image.ASLEEP``. Zwróć uwagę na wcięcie kodu po poleceniu ``while``
*takie jak w naszej liście zadań*.

Oczywiście, jeśli czas pracy jest równy lub większy niż 10 000 milisekund,
wówczas na ekranie pojawi się ``Image.SURPRISED``. Dlaczego? Ponieważ warunek
``while`` (ang. dopóki) będzie fałszywy (ang. False) (``running_time`` nie jest już ``< 10000``).
W takim przypadku pętla jest zakończona i program będzie kontynuowany po bloku
kodu pętli ``while``. Będzie to sprawiać wrażenie, że twoje urządzenie śpi przez 10 sekund
zanim obudzi się z zaskoczeniem na twarzy.

Spróbuj sam!

Obsługa zdarzenia
+++++++++++++++++

Jeśli chcemy aby MicroPython reagował na zdarzenia naciśnięcia przycisku,
musimy wprowadzić go w nieskończoną pętlę i sprawdzać w niej czy przycisk jest
wciśnięty (ang. ``is_pressed``).

Nieskończona pętla jest prosta::

    while True:
        # rób coś

(Pamiętaj, że ``while`` sprawdza czy coś jest ``True`` przed każdym wykonaniem
bloku kodu. Ponieważ ``True`` jest oczywiście ``True`` przez cały czas, to
otrzymujesz nieskończoną pętlę!)

Zróbmy bardzo proste elektroniczne zwierzątko. Jest ono smutne, gdy nie naciskasz
przycisku ``A``. A gdy wciśniesz przycisk ``B`` umiera. (Zdaję sobie
sprawę, że to nie jest zbyt przyjemna gra, więc może masz pomysł jak ją
ulepszyć.)::

    from microbit import *

    while True:
        if button_a.is_pressed():
            display.show(Image.HAPPY)
        elif button_b.is_pressed():
            break
        else:
            display.show(Image.SAD)

    display.clear()

Rozumiesz jak sprawdzić, które przyciski są wciśnięte? Użyliśmy ``if`` (ang. jeśli),
``elif`` (skrót od "else if") (ang. jeśli jednak) oraz ``else`` (ang. w pozostałych przypadkach).
Są one nazywane *warunkami* i
działają tak::

    if coś jest True:
        # zrób pierwszą rzecz
    elif coś innego jest True:
        # zrób następną rzecz
    else:
        # zrób jeszcze coś.

Prawie jak po polsku!

Metoda ``is_pressed`` generuje jeden z dwóch wyników: ``True`` albo ``False``.
Jeżeli przycisk jest wciśnięty, zwraca ``True``, w przeciwnym wypadku zwróci
``False``. Powyższy kod można przetłumaczyć jako "przez cały czas: jeśli
przycisk A jest wciśnięty - pokazuj szczęśliwą twarz, jeśli jednak przycisk
B jest wciśnięty - przerwij pętlę, a w pozostałych przypadkach pokaż smutną
minę". Przerywamy pętlę (zatrzymując działający przez cały czas program) za
pomocą instrukcji ``break`` (ang. przerwij).

Na samym końcu, kiedy elektroniczne zwierzątko nie żyje, czyścimy
(ang. ``clear``) ekran.

Wiesz jak uczynić tę grę mniej tragiczną? Jak sprawdziłabyś, czy *oba*
przyciski są wciśnięte? (Podpowiedź: Python ma operatory logiczne "i" (ang.
``and``), "lub" (ang. ``or``) oraz "nie" (ang .``not``), którymi można
sprawdzić wiele warunków (wyrażeń, które mają wartość ``True`` lub
``False``).

.. footer:: The image of Matrioshka dolls is licensed CC BY-SA 3.0, https://commons.wikimedia.org/w/index.php?curid=69402
