Obrazy
------

MicroPython jest tak dobry jak to tylko możliwe, jeśli chodzi o sztukę, jeśli
jedyne czym dysponujesz to macierz 5x5 diod LED (ang. Light Emitting Diodes,
diody emitujące światło na przodzie urządzenia). MicroPython daje sporo kontroli
nad wyświetlaczem, zatem możesz uzyskać sporo ciekawych efektów.

MicroPython posiada wbudowany zestaw obrazów które może pokazać na wyświetlaczu.
Na przykład, żeby pokazać na ekranie szczęśliwą buźkę musimy napisać::

    from microbit import *
    display.show(Image.HAPPY)

Mam nadzieję, że pamiętasz co robi pierwsza linijka powyżej. Druga linia używa
obiektu ``display`` i metody ``show`` (ang. pokaż) do wyświetlenia obrazka. Buźka
którą chcemy wyświetlić jest częścią obiektu ``Image`` (ang. Obraz) i nazywa się
``HAPPY`` (ang. szczęśliwy). Mówimy metodzie ``show`` by użyła tego obrazka przez
podanie jego nazwy w nawiasach (``(`` i ``)``).

.. image:: happy.png

Poniżej znajdziesz listę wszystkich wbudowanych obrazów:

    * ``Image.HEART``
    * ``Image.HEART_SMALL``
    * ``Image.HAPPY``
    * ``Image.SMILE``
    * ``Image.SAD``
    * ``Image.CONFUSED``
    * ``Image.ANGRY``
    * ``Image.ASLEEP``
    * ``Image.SURPRISED``
    * ``Image.SILLY``
    * ``Image.FABULOUS``
    * ``Image.MEH``
    * ``Image.YES``
    * ``Image.NO``
    * ``Image.CLOCK12``, ``Image.CLOCK11``, ``Image.CLOCK10``, ``Image.CLOCK9``,
      ``Image.CLOCK8``, ``Image.CLOCK7``, ``Image.CLOCK6``, ``Image.CLOCK5``,
      ``Image.CLOCK4``, ``Image.CLOCK3``, ``Image.CLOCK2``, ``Image.CLOCK1``
    * ``Image.ARROW_N``, ``Image.ARROW_NE``, ``Image.ARROW_E``,
      ``Image.ARROW_SE``, ``Image.ARROW_S``, ``Image.ARROW_SW``,
      ``Image.ARROW_W``, ``Image.ARROW_NW``
    * ``Image.TRIANGLE``
    * ``Image.TRIANGLE_LEFT``
    * ``Image.CHESSBOARD``
    * ``Image.DIAMOND``
    * ``Image.DIAMOND_SMALL``
    * ``Image.SQUARE``
    * ``Image.SQUARE_SMALL``
    * ``Image.RABBIT``
    * ``Image.COW``
    * ``Image.MUSIC_CROTCHET``
    * ``Image.MUSIC_QUAVER``
    * ``Image.MUSIC_QUAVERS``
    * ``Image.PITCHFORK``
    * ``Image.XMAS``
    * ``Image.PACMAN``
    * ``Image.TARGET``
    * ``Image.TSHIRT``
    * ``Image.ROLLERSKATE``
    * ``Image.DUCK``
    * ``Image.HOUSE``
    * ``Image.TORTOISE``
    * ``Image.BUTTERFLY``
    * ``Image.STICKFIGURE``
    * ``Image.GHOST``
    * ``Image.SWORD``
    * ``Image.GIRAFFE``
    * ``Image.SKULL``
    * ``Image.UMBRELLA``
    * ``Image.SNAKE``

Jest ich bardzo dużo! Może zmodyfikujesz kod powyżej żeby zobaczyć jak 
wyglądają pozostałe obrazy? (Wystarczy że zastąpisz ``Image.HAPPY`` jednym
z innych wbudowanych obrazów które są wypisane powyżej.)

Obrazy -- Zrób to sam
+++++++++++++++++++++

Naturalnie, na pewno chcesz stworzyć własny obrazek do wyświetlenia, prawda?

To proste.

Każda dioda LED (dalej nazywana pikselem) na wyświetlaczu może przyjąć jedną
z dziesięciu wartości. Jeśli piksel jest ustawiony na ``0`` (zero), to znaczy
że jest wyłączony. Po prostu jasność jest ustawiona na zero, dlatego nie świeci.
Jeśli jednak podamy wartość ``9`` to ustawiamy najwyższy poziom jasności.
Wartości od ``1`` do ``8`` reprezentują poziomy jasności między ``0`` (wyłączony)
do ``9`` (pełna jasność).

Mając powyższe na uwadze, możemy stworzyć własny obrazek w ten sposób::

    from microbit import *

    boat = Image("05050:"
                 "05050:"
                 "05050:"
                 "99999:"
                 "09990")

    display.show(boat)

(Kiedy uruchomisz urządzenie, na wyświetlaczu pokaże się łódka z dwoma masztami,
które będą nieco ciemniejsze od kadłuba.)

Wiesz już jak tworzyć obrazki? Widzisz jak każda linia wyświetlacza jest
reprezentowana przez ciąg znaków kończący się ``:`` (dwukropkiem) i zamknięty
w ``"`` (cudzysłów)? Każda liczba określa jasność. Mamy pięć linii po pięć
liczb, zatem możemy osobno nadać jasność każdemu pikselowi na urządzeniu. Tak
właśnie tworzy się własne obrazy.

Proste? Proste!

W zasadzie nie musisz podawać tych wartości w kilku liniach. Jeśli będzie to dla
ciebie czytelne, to możesz wszystkie wartości podać w jednej linii::

    boat = Image("05050:05050:05050:99999:09990")

Animacja
++++++++

Obrazki statyczne są zabawne, ale bardziej zabawne jest ich poruszenie. To też jest
niesamowicie proste do zrobienia w MicroPython ~ po prostu użyj listy obrazków!

Tu jest lista zakupów::

    Jaja
    Boczek
    Pomidory

Oto jak przedstawiłbyś tę listę w Python::

    zakupy = ["Jaja", "Boczek", "Pomidory" ]

Po prostu utworzyłem listę nazwaną ``zakupy`` i zawiera ona trzy elementy.
Python wie, że to jest lista ponieważ jest zawarta w kwadratowych nawiasach (``[`` i
``]``). Elementy w liście są oddzielone przecinkami (``,``) i w tej instancji
elementy są trzema ciągami znaków: ``"Jaja"``, ``"Boczek"`` i ``"Pomidory"``.
My wiemy, że są one ciągami znaków ponieważ są objęte znakami cudzysłowu ``"``.

W liście Python możesz przechowywać cokolwiek. Tu jest lista liczb::

    primes = [2, 3, 5, 7, 11, 13, 17, 19]

.. note::

    Liczby nie potrzebują być w cudzysłowie dopóki reprezentują wartość (w przeciwieństwie
    do ciągów znaków). Jest różnica pomiędzy ``2`` (numeryczna wartość 2) i ``"2"``
    (znak/cyfra reprezentująca liczbę 2). Nie martw się jeżeli nie widzisz w
    tym sensu teraz. Z czasem będzie to dla Ciebie oczywiste.

Jest nawet możliwe przechowywanie różnych rodzajów rzeczy w tej samej liście::

    mixed_up_list = ["hello!", 1.234, Image.HAPPY]

Zwróciłeś uwagę na ostatni element? To był obrazek!

Możemy powiedzieć MicroPythonowi, aby animował listę obrazków. Szczęśliwie mamy
już kilka wbudowanych list obrazków. Są to ``Image.ALL_CLOCKS`` i
``Image.ALL_ARROWS``::

    from microbit import *

    display.show(Image.ALL_CLOCKS, loop=True, delay=100)

Używamy ``display.show`` do pokazania listy obrazków na ekranie urządzenia
tak, jak w przypadku pojedynczego obrazka. Jednak mówimy MicroPythonowi użyj
``Image.ALL_CLOCKS`` i on rozumie, że musi pokazać każdy obrazek z listy
jeden po drugim. Rozkazujemy też MicroPythonowi aby powtarzał listę obrazków
(tak więc animacja trwa nieskończenie) przez ``loop=True``. Ponadto każemy mu,
aby opóźnienia pomiędzy każdym obrazkiem były tylko 100 milisekund (0,1
sekundy) w argumencie ``delay=100``.

Czy możesz domyślić się jak animować obrazki z listy ``Image.ALL_ARROWS``?
Jak możesz uniknąć nieskończonego powtarzania (podpowiedź: przeciwieństwem do
``True`` (ang. prawdziwy) jest ``False`` (ang. fałszywy) chociaż domyślna
wartość dla ``loop`` jest ``False``)? Czy potrafisz zmienić prędkość animacji?

Wreszcie tutaj możesz zobaczyć jak utworzyć swoją własną animację. W moim
przykładzie zamierzam stworzyć łódź tonącą na dno ekranu::

    from microbit import *

    boat1 = Image("05050:"
                  "05050:"
                  "05050:"
                  "99999:"
                  "09990")

    boat2 = Image("00000:"
                  "05050:"
                  "05050:"
                  "05050:"
                  "99999")

    boat3 = Image("00000:"
                  "00000:"
                  "05050:"
                  "05050:"
                  "05050")

    boat4 = Image("00000:"
                  "00000:"
                  "00000:"
                  "05050:"
                  "05050")

    boat5 = Image("00000:"
                  "00000:"
                  "00000:"
                  "00000:"
                  "05050")

    boat6 = Image("00000:"
                  "00000:"
                  "00000:"
                  "00000:"
                  "00000")

    all_boats = [boat1, boat2, boat3, boat4, boat5, boat6]
    display.show(all_boats, delay=200)

A tak działa ten kod:

* Utworzyłem sześć obrazków ``boat`` (ang. łódź) w dokładnie ten sam sposób, jak opisałem powyżej.
* Potem umieściłem wszystkie na liście, którą nazwałem ``all_boats``.
* W końcu poprosiłem ``display.show`` o animację listy z opóźnieniem 200 milisekund.
* Ponieważ nie użyłem ``loop=True`` łódź utonie tylko raz (to czyni moją animację naukowo poprawną). :-)

Co chciałbyś animować? Czy chciałbyś animować efekty specjalne? Jak byś zrobił
aby obrazek znikał, a potem pojawiał się znowu?
