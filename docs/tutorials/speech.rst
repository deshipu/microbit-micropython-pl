Mowa
----

.. warning::

    UWAGA! TO JEST KOD ALFA!

    Zastrzegamy sobie prawo do zmiany tego interfejsu API w miarę rozwoju oprogramowania.

    Jakość mowy nie jest świetna, tylko "wystarczająco dobra". Ze względu na ograniczenia urządzenia, mogą wystąpić błędy pamięci i / lub nieoczekiwane dodatkowe dźwięki podczas odtwarzania. To są dopiero początki i cały czas poprawiamy kod syntezatora mowy. Zgłaszanie błędów będzie mile widziane.

Komputery i roboty, które mówią wydają się bardziej "ludzkie".

Często o tym co komputer właśnie robi dowiadujemy się poprzez graficzny interfejs użytkownika (ang. graphical user interface, GUI). W przypadku BBC micro:bit, GUI to matryca LED 5x5, która pozostawia wiele do życzenia.

Sprawienie, aby micro:bit mówił, jest jednym ze sposobów na wyrażenie informacji w zabawny, skuteczny i użyteczny sposób. W tym celu zintegrowaliśmy prosty syntezator mowy oparty na zdekonstruowanej wersji syntezatora z wczesnych lat osiemdziesiątych. Brzmi on naprawdę uroczo, w stylu "wszyscy ludzie muszą umrzeć".

Mając to na uwadze, użyjemy syntezatora do stworzenia...

Poezji DALEKów
++++++++++++++

.. image:: dalek.jpg

Mało kto wie, że DALEKowie lubią poezję -- szczególnie limeryki. Szaleją na punkcie wierszy z anapestycznym metrum o surowej budowie AABBA. Kto by pomyślał!

(Jak się niżej dowiemy, to wina Doktora, że, ku irytacji Davrosa, DALEKowie lubią limeryki.)

W każdym razie, zamierzamy stworzyć recital poezji DALEKowej na żądanie.

Powiedz coś
+++++++++++

Zanim urządzenie będzie mogło mówić, musisz podłączyć głośniczek w taki sposób:

.. image:: ../speech.png

Najłatwiejszym sposobem na to żeby urządzenie zaczęło mówić jest zaimportowanie modułu ``speech`` (pol. ``mowa``) i użycie funkcji ``say`` (pol. ``powiedz``) w taki sposób:: 

    import speech

    speech.say("Hello, World")

Jest to urocze, jednak nie jest wystarczająco DALEKowate jak na nasz gust, dlatego musimy zmienić niektóre parametry używane przez syntezator do wygenerowania mowy. Nasz syntezator mowy jest pod tym względem dość potężny, ponieważ możemy zmienić cztery parametry:

* ``pitch`` (pol. ``ton``) - jak wysoko lub nisko brzmi głos (0 = wysoko, 255 = Barry White)
* ``speed`` (pol. ``szybkość``) - jak szybko urządzenie mówi (0 = niemożliwe, 255 = opowiadanie na dobranoc)
* ``mouth`` (pol. ``usta``) - czy mowa jest przez zaciśnięte zęby czy bardzo wyraźna (0 = kukiełka brzuchomówcy, 255 = Kurak Leghorn)
* ``throat`` (pol. ``gardło``) - jak spokojny lub napięty jest ton głosu (0 = załamujący się, 255 = kompletnie rozluźniony)

W sumie razem parametry te kontrolują jakość dźwięku -- tj. barwę dźwięku. Szczerze mówiąc, najlepszą drogą do uzyskania pożądanej barwy dźwięku jest eksperymentowanie, ocena i dostosowanie.

Aby dostosować ustawienia, przekazujesz je jako argumenty funkcji ``say``. Więcej szczegółów można znaleźć w dokumentacji interfejsu API ``speech``.

Po kilku przeprowadzonych eksperymentach, ten brzmi całkiem DALEKowato::

    speech.say("I am a DALEK - EXTERMINATE", speed=120, pitch=100, throat=100, mouth=200)

Poezja na Żądanie
+++++++++++++++++

Będąc cyborgami, DALEKowie wykorzystują umiejętności robotów do tworzenia poezji
i okazuje się, że korzystają z algorytmów napisanych w Pythonie, np::

    # Generator poezji DALEKowej Doktora
    import speech
    import random
    from microbit import sleep

    # Losowo wybierz fragmenty do wstawienia do szablonu.
    location = random.choice(["brent", "trent", "kent", "tashkent"])
    action = random.choice(["wrapped up", "covered", "sang to", "played games with"])
    obj = random.choice(["head", "hand", "dog", "foot"])
    prop = random.choice(["in a tent", "with cement", "with some scent",
                         "that was bent"])
    result = random.choice(["it ran off", "it glowed", "it blew up",
                           "it turned blue"])
    attitude = random.choice(["in the park", "like a shark", "for a lark",
                             "with a bark"])
    conclusion = random.choice(["where it went", "its intent", "why it went",
                               "what it meant"])

    # Szablon wiersza. Nawiasy {} będą zastąpione nazwanymi fragmentami. 
    poem = [
        "there was a young man from {}".format(location),
        "who {} his {} {}".format(action, obj, prop),
        "one night after dark",
        "{} {}".format(result, attitude),
        "and he never worked out {}".format(conclusion),
        "EXTERMINATE",
    ]

    # Wprowadź w pętlę każdą linię wiersza i użyj modułu
    for line in poem:
        speech.say(line, speed=120, pitch=100, throat=100, mouth=200)
        sleep(500)

Jak pokazują komentarze, jest to bardzo prosty model:

* Nazwane fragmenty (``location``, ``prop``, ``attitude`` itd.) są generowane losowo z predefiniowanych list możliwych wartości. Zwróć uwagę na użycie ``random.choice`` w celu wybrania pojedynczego elementu z listy.
* Szablon wiersza definiowany jest jako lista zwrotek z "dziurami" (oznaczonymi przez ``{}``), do których za pomocą metody ``format`` wstawione zostaną nazwane fragmenty.
* Na koniec, Python przechodzi po wszystkich elementach na liście wypełniaczy poezji i używa ``speech.say`` z ustawieniami głosu DALEKa do recytowania wiersza. Między poszczególnymi liniami wstawiana jest pauza 500 milisekund, ponieważ nawet DALEKowie muszą odetchnąć.

Co ciekawe, oryginalne wytyczne związane z poezją zostały napisane przez
Davrosa w języku `FORTRAN <https://en.wikipedia.org/wiki/Fortran>`_
(odpowiedni język dla DALEKów, gdyż pisany jest TYLKO WIELKIMI LITERAMI). Jednakże
Doktor cofnął się w czasie dokładnie do punktu pomiędzy wprowadzaniem
`testów jednostkowych <https://pl.wikipedia.org/wiki/Test_jednostkowy>`_ Davros'a i
`potoków wdrożeniowych <https://en.wikipedia.org/wiki/Continuous_delivery>`_ .
Wówczas był w stanie umieścić interpreter MicroPythona w systemie
operacyjnym DALEKA i powyżej widzisz zawarty w bankach pamięci DALEKA kod z
`ukrytą niespodzianką <https://pl.wikipedia.org/wiki/Easter_egg>`_ czy też
`rickrollem <https://www.youtube.com/watch?v=dQw4w9WgXcQ>`_ od Władcy Czasu.

Fonemy
++++++

Zauważysz, że funkcja ``say`` nie tłumaczy dokładnie słów na odpowiednie dźwięki. Aby mieć lepszą kontrolę nad rezultatem, użyj fonemów: podstawowej jednostki struktury fonologicznej mowy.

Korzyść z używania fonemow jest taka, że nie musisz wiedzieć jak się poszczególne wyrazy pisze. Musisz tylko wiedzieć jak się to słowo wymawia, aby zapisać je fonetycznie.

Pełna lista fonemów rozumianych przez syntezator mowy znajduje się w dokumentacji API dla mowy. Ewentualnie, zaoszczędź sobie dużo czasu wprowadzając angielskie słowa do funkcji ``translate`` (pol. przetłumacz). Zwróci ona pierwsze przybliżenie fonemów, które micro:bit wykorzystałby do wygenerowania audio. Otrzymany rezultat może zostać ręcznie zmodyfikowany, żeby poprawić dokładność, fleksję i akcent (tak aby brzmiał bardziej naturalnie).

Funkcja ``pronounce`` (pol. wymówić) jest używana do wyprowadzania fonemu w następujący sposób::

    speech.pronounce("/HEH5EH4EH3EH2EH2EH3EH4EH5EHLP.”)

Jak udoskonaliłbyś kod Doktora, aby używał fonemów?

Zaśpiewaj Piosenkę Micro:bit'a
++++++++++++++++++++++++++++++

Poprzez zmianę ustawień ``pitch`` (pol. ton) i wywołanie funkcji ``sing`` (pol. śpiewaj), urządzenie może zacząć śpiewać (jednakże bez szans na wygranie Eurowizji, póki co).

Mapowanie z numerów tonów na nuty jest pokazane poniżej:

.. image:: ../speech-pitch.png

Funkcja ``sing`` musi przyjąć jako dane wejściowe fonemy i tonację::

    speech.sing("#115DOWWWW")

Zwróć uwagę na to, w jaki sposób fonemy poprzedzone są wysokością dźwięku z symbolem kratki (``#``). Tonacja pozostanie taka sama dla kolejnych fonemów do momentu wprowadzenia nowej tonacji.

Poniższy przykład pokazuje jak wszystkie trzy funkcje generujące (``say``,
``pronounce`` oraz ``sing``) mogą zostać wykorzystane do stworzenia czegoś przypominającego mowę.

.. include:: ../../examples/speech.py
    :code: python

.. footer:: Obraz DALEKa jest licencjonowany na zasadach przestawionych poniżej: https://commons.wikimedia.org/wiki/File:Dalek_(Dr_Who).jpg Obraz DAVROSa jest licencjonowany na zasadach przedstawionych poniżej: https://en.wikipedia.org/wiki/File:Davros_and_Daleks.jpg
