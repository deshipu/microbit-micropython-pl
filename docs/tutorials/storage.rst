Przechowywanie danych
---------------------

Czasami potrzebujesz trwale zachować użyteczne informacje. Takie informacje
przechowywane są jako dane (cyfrowa reprezentacja informacji przechowywanych
na komputerze). Zachowane na komputerze dane powinny przetrwać nawet
jeśli wyłączysz i ponownie włączysz urządzenie.

Na szczęście MicroPython na minikomputerze micro:bit pozwala Ci to osiągnąć
za pomocą prostego systemu plików. Z powodu ograniczeń pamięci, na system
plików dostępne jest tylko **około 30k**.

Czym jest system plików?

To sposób przechowywania i organizowania danych w sposób trwały - dane zapisane
w systemie plików powinny przetrwać restart urządzenia. Tak jak sugeruje to
nazwa dane zapisywane w systemie plików przechowywane są jako pliki.

.. image:: files.jpg
(W języku angielskim słowo file, tłumaczone jako
plik, oznacza także dokument - przyp. tłum.)

Plik (komputerowy) jest posiadającym nazwę zasobem cyfrowym, który
przechowywany jest w systemie plików. Zasoby takie przechowują użyteczne
informacje jako dane. To swego rodzaju oznakowany pojemnik
przechowujący informacje. Zazwyczaj nazwa pliku oddaje to co plik zawiera.
Zwyczajowo nazwy plików komputerowych kończy się sufiksem ``.coś``. Zazwyczaj
to ``.coś`` wskazuje jaki typ danych został użyty do reprezentacji informacji.
Na przykład, ``.txt`` oznacza plik tekstowy, ``.jpg`` obraz w formacie JPEG
a ``.mp3`` dane dźwiękowe przetworzone do postaci cyfrowej algorytmem MP3.

Niektóre systemy plików (taki jak ten na Twoim laptopie
albo komputerze stacjonarnym) pozwalają na organizowanie plików
w katalogi -- posiadające nazwę pojemniki, które grupują powiązane ze sobą
pliki i podkatalogi. Jednakże *system plików dostępny w MicroPythonie
jest płaskim systemem plików*. Płaski system plików nie posiada
katalogów -- wszystkie Twoje pliki są po prostu przechowywane
w jednym i tym samym miejscu.

Język programowania Python zawiera łatwe w użyciu i bardzo skuteczne metody
pracy z komputerowym systemem plików. W MicroPythonie na minikomputerze
micro:bit zaimplementowano użyteczny podzbiór tych metod. Pozwalają one
w łatwy sposób odczytywać i zapisywać pliki z i do urządzenia, jednocześnie
zapewniając zgodność z innymi wersjami Pythona.

.. warning::

    Wgrywanie programów na minikomputer micro:bit KASUJE WSZYSTKIE DANE
    ponieważ operacja ta nadpisuje pamięć flash używaną przez urządzenie,
    a system plików także jest w niej przechowywany.

    Jeżeli jedynie wyłączysz swoje urządzenie, dane pozostaną nienaruszone
    do czasu, aż je usuniesz albo załadujesz na urządzenie nowy program.

Sezamie otwórz się
++++++++++++++++++

Odczyt i zapis w systemie plików wykonywany jest za pomocą funkcji
``open`` (ang. otwórz). Kiedy plik jest już otwarty możesz z nim robić rozmaite rzeczy, do
czasu aż go zamkniesz. To bardzo ważne abyś zamykał pliki po to, żeby MicroPython
wiedział, że skończyłeś z nimi pracować.

Aby mieć pewność, że tak się stanie najlepszym sposobem jest użycie
instrukcji ``with`` w następujący sposób::

    with open('story.txt') as my_file:
        content = my_file.read()
    print(content)

Instrukcja ``with`` używa funkcji ``open`` aby otworzyć plik i przypisać go
do obiektu. W powyższym przykładzie funkcja ``open`` otwiera plik ``story.txt``
(zapewne tekstowy plik z jakąś historyjką [ang. story - opowieść]).
Obiekt, który w Pythonie reprezentuje ten plik nazywa się ``my_file``
(ang. mój_plik). Następnie, we wciętej linijce programu pod instrukcją ``with``,
obiekt ``my_file`` zostaje użyty aby odczytać (funkcja ``read()``) zawartość
pliku i przypisać ją do obiektu ``content``.

Ważna uwaga: *następna linijka zawierająca instrukcję* ``print`` *nie jest
wcięta*. Blok programu związany z instrukcją ``with`` złożony jest tylko
z jednej linijki wczytującej plik. Jak tylko blok programu związany
z instrukcją ``with`` zostanie zamknięty Python (a także MicroPython)
automatycznie zamknie plik za Ciebie. To tak zwana obsługa kontekstu -- funkcja
``open`` tworzy obiekty, które są identyfikatorami kontekstu dla plików.

Mówiąc prościej, zakres programu, w którym operujesz na pliku jest związany
z blokiem instrukcji ``with``, która służy do jego otwarcia.

Zdezorientowany?

Niepotrzebnie. Mówię po prostu, że Twój program powinien wyglądać
w następujący sposób:

    with open('some_file') as some_object:
        # W tym bloku programu, związanym z instrukcją ``with``,
        # zrób coś z obiektem some_object.

    # Kiedy MicroPython dojdzie do końca tego bloku,
    # automatycznie zamknie plik za Ciebie.

Plik komputerowy otwieramy z dwóch powodów -- aby odczytać jego zawartość
(jak to pokazano powyżej), albo żeby do niego coś zapisać. Domyślnym trybem jest
tryb odczytu. Jeśli chcesz pisać do pliku musisz powiedzieć o tym funkcji
``open`` w następujący sposób:

    with open('hello.txt', 'w') as my_file:
        my_file.write("Hello, World!")

Zwróć uwagę na argument ``'w'``, który został użyty aby ustawić obiekt
``my_file`` w tryb zapisu. Aby ustawić obiekt pliku w tryb odczytu, możesz
przekazać argument ``'r'``, ale ponieważ jest to zachowanie domyślne rzadko się
to robi.

Zapis danych do pliku odbywa się za pomocą metody (dobrze odgadłeś) ``write`` (ang. pisz).
Przyjmuje ona, jako argument, łańcuch znaków (ang. string), który chcesz zapisać
do pliku. W powyższym przykładzie zapisałem do pliku "hello.txt" napis
"Hello, World!".

Proste!

.. note::

    Kiedy otwierasz plik aby do niego pisać (możliwe, że nawet wielokrotnie,
    dopóki jest otwarty) będziesz nadpisywać jego zawartość jeśli plik już
    istnieje.

    Jeśli chcesz dodać dane do pliku powinieneś/powinnaś najpierw go wczytać,
    zachować gdzieś jego zawartość, zamknąć go, dodać (nowe) dane do zachowanej
    zawartości a następnie otworzyć plik ponownie i wpisać uaktualnioną
    zawartość.

    Tak właśnie postępuje MicroPython; "zwyczajny" Python potrafi otwierać
    pliki w trybie dodawania ("append"). Powodem, dla którego nie możemy tego
    zrobić na minikomputerze micro:bit jest uproszczony sposób implementacji
    systemu plików.

Na pomoc systemie operacyjny
++++++++++++++++++++++++++++

Oprócz czytania z i pisania do plików, Python potrafi także wykonywać z nimi
inne operacje. Z pewnością chcesz wiedzieć jakie pliki znajdują się w systemie
plików, a czasami także je z niego usunąć.

Na zwykłym komputerze, w imieniu Pythona, to system operacyjny (taki jak
Windows, OSX czy Linux) zarządza plikami. W Pythonie odpowiednie do tego funkcje
dostępne są za pośrednictwem modułu ``os``. Ponieważ jednak sam MicroPython
**jest** systemem operacyjnym postanowiliśmy, dla spójności, pozostawić
te funkcje w module ``os``, tak abyś wiedział(a) gdzie je znaleźć gdy będziesz
używać ``normalnej`` wersji Pythona na urządzeniach takich jak laptop
czy Raspberry Pi.

Zasadniczo możesz wykonać trzy operacje związane z systemem plików: uzyskać
listę plików, usunąć plik oraz zapytać o rozmiar pliku.

Aby uzyskać listę plików w Twoim systemie plików użyj funkcji ``listdir``.
Zwraca ona listę łańcuchów znakowych reprezentujących nazwy plików::

    import os
    my_files = os.listdir()

Aby skasować plik użyj funkcji ``remove`` (ang. usuń). Przyjmuje ona jako argument łańcuch
znakowy reprezentujący nazwę pliku, który chcesz skasować w następujący sposób::

    import os
    os.remove('filename.txt')

Wreszcie, czasami przydaje się wiedzieć jak duży jest plik zanim rozpocznie się
jego wczytywanie. Osiągniesz to używając funkcji ``size`` (ang. wielkość). Tak jak funkcja
``remove`` przyjmuje ona łańcuch znaków reprezentujący nazwę pliku, którego
rozmiar chcesz poznać. Funkcja zwraca wartość całkowitą
oznaczającą liczbę bajtów, które zajmuje plik::

    import os
    file_size = os.size('a_big_file.txt')

Bardzo fajnie, że na minikomputerze dostępny jest system plików, ale co
jeśli chcemy pobrać z niego albo załadować na niego plik z zewnątrz?

Użyj po prostu narzędzia ``microfs``!

Przesyłanie plików
++++++++++++++++++

Jeśli na komputerze, którego używasz do oprogramowywania swojego
BBC micro:bit, masz zainstalowanego Pythona, możesz użyć specjalnego narzędzia
zwanego ``microfs`` (nazywanego skrótowo ``ufs`` jeśli używany jest
z linii komend). Instrukcję instalacji i pełny opis użycia wszystkich funkcji
znajdziesz `w dokumentacji tego narzędzia <https://microfs.readthedocs.io>`_.

Niemniej jednak większość potrzebnych rzeczy można wykonać za pomocą czterech
prostych poleceń::

    $ ufs ls
    story.txt

Komenda ``ls`` wyświetla listę plików znajdujących się w systemie plików
(została nazywa tak samo jak dobrze znana Uniksowa komenda ``ls``,
która ma dokładnie to samo zadanie).

::

    $ ufs get story.txt

Komenda ``get`` pobiera plik z podłączonego minikomputera micro:bit i zapisuje
go do bieżącego katalogu na Twoim komputerze (nazwana została tak samo jak
komenda ``get`` popularnego protokołu przesyłu plików -- FTP, która spełnia
to samo zadanie).

::

    $ ufs rm story.txt

Komenda ``rm`` usuwa plik o podanej nazwie z systemu plików na podłączonym
micro:bit (nazwana została tak samo jako komanda Uniksowa,
która spełnia to samo zadanie).

::

    $ ufs put story2.txt

W końcu komenda ``put`` umieszcza plik z komputera na podłączonym do niego
micro:bit (nazywa się tak jak, wykonująca tę samą funkcję,
komenda protokołu FTP).

Głównie main.py
+++++++++++++++

System plików ma ciekawą cechę - jeśli na urządzenie załadujesz jedynie
środowisko uruchomieniowe MicroPython, po włączeniu czeka
ono po prostu na wykonanie jakichś poleceń. Jednakże, jeśli skopiujesz
również specjalny plik nazwany ``main.py`` (ang. main: główny), po restarcie
urządzenia MicroPython wykona zawartość tego specjalnego pliku.

Dodatkowo jeśli przekopiujesz inne pliki Pythona do systemu plików
minikomputera, możesz je zaimportować (``import``) tak jak każdy moduł
Pythona. Na przykład gdybyś miał plik ``hello.py`` zawierający następujący
program::

    def say_hello(name="World"):
        return "Hello, {}!".format(name)

...mógłbyś zaimportować i użyć funkcji ``say_hello`` w następujący sposób::

    from microbit import display
    from hello import say_hello

    display.scroll(say_hello())

Oczywiście wynikiem będzie napis "Hello, World!" przewijający się przez
wyświetlacz. Ważne jest, że w tym przykładzie funkcje rozdzielone są na dwa
moduły a instrukcja ``import`` służy do współdzielenia kodu.

.. note::
    Jeśli, na urządzenie, oprócz środowiska uruchomieniowego
    wgrałeś także skrypt, MicroPython zignoruje plik ``main.py`` i zamiast tego
    wykona polecenia ze skryptu.

    Aby wgrać tylko środowisko uruchomieniowe, upewnij się że skrypt, który
    wpisałeś w edytorze, jest pusty (nie ma w nim żadnych znaków). Po
    załadowaniu będziesz mógł przekopiować plik ``main.py``.

.. footer:: Obraz teczek na dokumenty został użyty zgodnie z licencją Creative Commons License i jest dostępny pod adresem: https://www.flickr.com/photos/jenkim/2270085025
