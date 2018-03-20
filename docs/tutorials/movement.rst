Ruch
----

BBC micro:bit ma wbudowany akcelerometr. Mierzy on ruch wzdłuż trzech osi:

*X - przechylanie od lewej do prawej.
*Y - przechylanie do przodu i do tyłu.
*Z - poruszanie górę i w dół.

Dla każdej z osi jest metoda zwracająca liczbę dodatnią lub ujemną, wskazując pomiar w mili-g. Kiedy wyświetlacz pokazuje 0, oznacza to, że przyrząd jest równoległy do danej osi.

Poniższy przykład pokazuje bardzo prostą poziomicę wykorzystującą metodę ``get_x`` mierzącą jak bardzo urządzenie jest wypoziomowane względem osi X.

    from microbit import *

    while True:
        reading = accelerometer.get_x()
        if reading > 20:
            display.show("R")
        elif reading < -20:
            display.show("L")
        else:
            display.show("-")

Jeżeli trzymasz urządzenie płasko, powinno ono wyświetlić ``-``; jednak jeżeli tylko obrócisz je w lewo lub w prawo, pokaże ono odpowiednio ``L`` lub ``R``.

Chcemy, aby urządzenie natychmiastowo reagowało na zmiany, dlatego też użyliśmy nieskończonej pętli ``while``. Pierwsza rzecz, która stanie się *w ciele pętli*, to pomiar wzdłuż osi X nazwany ``reading`` (pol. odczyt). Ponieważ akcelerometr jest *bardzo* czuły, urządzenie jest uznane za wypoziomowane kiedy wartości znajdują się w granicy +/-20. Dlatego właśnie warunki ``if`` oraz ``elif`` sprawdzają dla wartości ``>20`` oraz ``<-20``. Wyrażenie ``else`` oznacza, że jeżeli ``reading`` znajduje się pomiędzy -20 i 20, to urządzenie uważane jest za wypoziomowane. Dla każdego z tych warunków do pokazania odpowiednich znaków używamy wyświetlacza.

Istnieje również metoda ``get_y`` dla osi Y oraz ``get_z`` dla osi Z.

Zastanawiałeś się kiedyś w jaki sposób telefon komórkowy rozpoznaje w którą stronę jest zwrócony i w jaki sposób ma być zorientowany wyświetlany obraz na ekranie? Potrafi to właśnie dzięki wbudowanemu akcelerometrowi działającemu dokładnie jak ten w powyższym programie. Kontrolery gier również zawierają akcelerometry umożliwiające sterowanie i poruszanie się w grach.

Muzyczny Zamęt
++++++++++++++

Jednym z najcudowniejszych aspektów MicroPython na BBC micro:bit jest łatwość z jaką można łączyć różne możliwości tego urządzenia. Na przykład zamieńmy go (w pewnym sensie) w instrument muzyczny.

Podłącz głośnik zgodnie z instrukcją w rozdziale Muzyka. Użyj krokodylków. Połącz styki 0 oraz GND z dodatnim i ujemnym wejściem głośnika -- nie ma znaczenia które wejście z którym stykiem zostanie połączone.

.. image:: pin0-gnd.png

Co się stanie jak wykorzystamy odczyty z akcelerometru i stworzymy na ich podstawie dźwięki o danym tonie? Przekonajmy się::

    from microbit import *
    import music

    while True:
        music.pitch(accelerometer.get_y(), 10)

Kluczowa linijka znajduje się na końcu i jest niewiarygodnie prosta. *Zagnieżdżamy* odczyt z osi Y jako częstotliwość wprowadzaną do metody ``music.pitch``. Ponieważ chcemy, żeby ton był zmieniany tak szybko jak urządzenie jest przechylane, pozwalamy mu grać tylko przez 10 milisekund. Dzięki temu, że urządzenie jest w niekończącej się pętli ``while``, nieustannie reaguje na zmiany w odczytach osi Y.

To wystarczy!

Przechyl urządzenie do przodu i do tyłu. Jeżeli odczyt wzdłuż osi Y jest dodatni, zmieni wysokość dźwięku granego przez micro:bit.

Wyobraź sobie całą orkiestrę symfoniczną takich urządzeń. Możesz zagrać melodię? Jakie zmiany wprowadziłbyś do programu, aby micro:bit brzmiał bardziej muzykalnie? 
