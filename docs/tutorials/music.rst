Muzyka
------

MicroPython na BBC micro:bit zawiera bogaty w możliwości moduł muzyki i dźwięku. Dzięki niemu można w prosty sposób zaprogramować BBC micro:bit do wygenerowania
piśnięć i innych odgłosów. Oczywiście, aby coś usłyszeć trzeba *podłączyć głośniki* -- za pomocą krokodylków podłącz pin 0 oraz GND do wejść głośnika. Nie ma znaczenia który zacisk do którego wejścia zostanie podłączony.

.. image:: pin0-gnd.png

.. note::

    Do tego celu nie używaj brzęczyka piezoelektrycznego, który może generować
    tylko pojedynczy ton.

Zagrajmy coś!::

    import music

    music.play(music.NYAN)

Zauważ, że importujemy moduł ``music``. Zawiera on polecenia wykorzystywane do
wytwarzania i kontrolowania dźwięków.

MicroPython ma dość dużo wbudowanych melodii. Oto ich kompletna lista:

* ``music.DADADADUM``
* ``music.ENTERTAINER``
* ``music.PRELUDE``
* ``music.ODE``
* ``music.NYAN``
* ``music.RINGTONE``
* ``music.FUNK``
* ``music.BLUES``
* ``music.BIRTHDAY``
* ``music.WEDDING``
* ``music.FUNERAL``
* ``music.PUNCHLINE``
* ``music.PYTHON``
* ``music.BADDY``
* ``music.CHASE``
* ``music.BA_DING``
* ``music.WAWAWAWAA``
* ``music.JUMP_UP``
* ``music.JUMP_DOWN``
* ``music.POWER_UP``
* ``music.POWER_DOWN``

Pobierz któryś z przykładowych kodów i odtwórz melodię. Która podoba Ci się najbardziej? Masz pomysł na ich wykorzystanie jako sygnały?

Wolfgang Amadeusz Microbit
++++++++++++++++++++++++++

Zaprogramowanie swojej własnej melodii jest bardzo łatwe!

Każda nuta ma nazwę (np. ``C#`` lub ``F``), oktawę (określającą jak wysoko lub nisko dźwięk ma być grany) oraz długość (przez jaki czas dźwięk ma być grany). Oktawy są oznaczone liczbami ~ 0 oznacza najniższą oktawę, oktawa 4 zawiera środkowe C, a 8 jest tak wysoko, że wyższej już nie będziesz potrzebować, chyba że zechcesz tworzyć muzykę dla psów. Długość dźwięku jest również wyrażana jako liczby. Im większa liczba tym dłużej nuta będzie odtwarzana. Te wielkości są od siebie zależne, np. po wprowadzeniu wartości ``4``, nuta będzie odtwarzana 2 razy dłużej niż po wprowadzeniu ``2`` itd. Jeśli zamiast nuty wpiszesz "R", to MicroPython w tym miejscu zrobi pauzę (ang. rest) o zadanej długości.

Każda nuta opisywana jest jako ciąg znaków::

    NUTA[oktawa][:długość]

Na przykład, ``"A1:4"`` opisuje nutę ``A`` w oktawie numer ``1`` o długości
``4``.

Utwórz listę nut, które stworzą melodię. Poniżej znajduje się zapis, dzięki 
któremu MicroPython zagra początek melodii "Panie Janie"::

    import music

    tune = ["C4:4", "D4:4", "E4:4", "C4:4", "C4:4", "D4:4", "E4:4", "C4:4",
            "E4:4", "F4:4", "G4:8", "E4:4", "F4:4", "G4:8"]
    music.play(tune)

.. note::

    MicroPython umożliwia zapisywanie takich melodii w uproszczony sposób. Zapamięta oktawę oraz długość nuty i będzie je wykorzystywał aż do wprowadzenia nowych wartości. Dzięki temu powyższy przykład może zostać zapisany tak:

        import music

        tune = ["C4:4", "D", "E", "C", "C", "D", "E", "C", "E", "F", "G:8",
 
               "E:4", "F", "G:8"]
        music.play(tune)

    Zauważ, że wartości określające oktawę i czas trwania są wpisywane tylko wtedy, kiedy są zmieniane. Dzięki temu kod jest łatwiejszy zarówno do napisania jak i do odczytania.

Efekty dźwiękowe
++++++++++++++++

MiroPython umożliwia tworzenie melodii i dźwięków zapisanych inaczej niż nutami. 
Na przykład dzięki poniższemu kodowi możemy uzyskać efekt syreny policyjnej::

    import music

    while True:
        for freq in range(880, 1760, 16):
            music.pitch(freq, 6)
        for freq in range(1760, 880, -16):
            music.pitch(freq, 6)


Zwróć uwagę, że w tym przypadku użyliśmy metody ``music.pitch``.
Wymaga ona podania częstotliwości. Na przykład częstotliwość 440 to koncertowe A używane do strojenia instrumentów w orkiestrze symfonicznej.

W powyższym przykładzie funkcja ``range`` (ang. zakres) jest wykorzystana do wygenerowania zakresów numerycznych wartości. Te liczby są użyte do zdefiniowania wysokości tonu. Te trzy argumenty dla funkcji ``range`` to odpowiednio wartość początkowa zakresu, wartość końcowa i krok. Zatem pierwsze użycie ``range``, mówi po polsku "utwórz przedział liczb pomiędzy 880 a 1760 o kroku 16". Drugie użycie ``range`` mówi "utwórz przedział wartości pomiędzy 1760 a 880 o kroku -16". W ten sposób uzyskamy zakres częstotliwości, które stopniowo zwiększając się i zmniejszając tworzą dźwięk przypominający syrenę.

Ponieważ dźwięk syreny powinien trwać nieskończenie długo, jest on wpisany
w niekończącą się pętlę ``while``.

Co ważne, wprowadziliśmy nowy rodzaj pętli wewnątrz pętli ``while`` (ang. dopóki): pętlę ``for`` (ang. dla). Po polsku to jest tak, jak powiedzieć "dla każdego elementu w pewnym zbiorze, wykonaj z nim pewną czynność". Konkretnie w powyższym przypadku to oznacza "dla każdej częstotliwości w określonym w zakresie, graj ton o tej częstotliwości przez 6 milisekund". Zwróć uwagę na wcięcia przy każdym wierszu wewnątrz pętli ``for`` (mówiliśmy o tym wcześniej), sprawiają one, że Python dokładnie wie, który kod uruchomić aby obsłużyć poszczególne elementy.
