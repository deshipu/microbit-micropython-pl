Hello, World!
-------------

Tradycyjnie, pierwszym krokiem w nauce nowego języka programowania jest stworzenie
aplikacji, która wyświetli komunikat "Witaj świecie!" (ang. "Hello, World").


.. image:: ../scroll-hello.gif

To proste z MicroPythonem::

    from microbit import *
    display.scroll("Hello, world!")

Każdy wiersz ma swoje znaczenie. Pierwszy z nich::

    from microbit import *

...mówi MicroPythonowi, by zaimportował wszystkie rzeczy potrzebne do pracy
z BBC micro:bit. Wszystko to jest w module ``microbit`` (moduł to biblioteka
z wcześniej przygotowanym kodem). Poleceniem ``import`` mówisz MicroPythonowi,
że chcesz użyć danego modułu, a ``*`` to sposób Pythona na określenie *wszystkiego*.
Zatem ``from microbit import *`` oznacza "chcę użyć wszystkiego co jest dostępne
w bibliotece microbit".

Druga linia::

    display.scroll("Hello, world!")
    
...mówi MicroPythonowi, by wyświetlił przesuwający się ciąg znaków "Hello, 
world!". ``display`` w tym przypadku to *obiekt*
(ang. object) z modułu ``microbit``, który reprezentuje fizyczny wyświetlacz
urządzenia (mówimy "obiekt" zamiast "rzecz" lub "to coś").
By wydać wyświetlaczowi polecenie, po kropce ``.`` podajemy komendę -- tak
naprawdę takie polecenia nazywamy *metodami* (ang. method). W tym przypadku
używamy polecenia ``scroll`` (ang. przewiń). Polecenie ``scroll``
musi wiedzieć jakie znaki pokazać na wyświetlaczu. Wpisujemy je ujęte
w cudzysłów (``"``) i zamknięte w nawiasy (``(`` i ``)``). W programowaniu to
co przekazujemy do metody nazywamy *argumentami* (ang. arguments). Zatem 
``display.scroll("Hello, world!")`` oznacza, po polsku, "chcę użyć 
wyświetlacza by pokazać przesuwający się tekst 'Hello, world!'". Jeśli metoda
nie potrzebuje żadnych argumentów, musimy to jasno określić używając pustych 
nawiasów: ``()``.

Skopiuj powyższy kod do swojego edytora i wgraj go (ang. flash) do urządzenia.
Czy domyślasz się jak zmienić wyświetlany tekst? Czy możesz go zmienić tak, 
by przywitał ciebie? Na przykład, chciałbym by tekst brzmiał "Witaj, Andrzeju!". 
Mała podpowiedź: musisz zmienić argument metody ``scroll``.

.. warning::

    To może nie działać :-)
    
    Tutaj zaczyna się prawdziwa zabawa, a MicroPython stara się być naprawdę
    pomocny. Jeśli napotka błąd, to na wyświetlaczu pokaże komunikat błędu.
    W miarę możliwości, pokaże również numer linii kodu, która zawiera błąd.

    Python oczekuje, że wprowadzisz **BEZBŁĘDNY** kod. Na przykład, ``Microbit``,
    ``microbit`` i ``microBit`` są przez Pythona traktowane jak trzy osobne
    rzeczy. Jeśli w treści błędu zobaczysz ``NameError`` (błąd nazwy), oznacza
    to że prawdopodobnie wpisana nazwa została podana niedokładnie. To jak różnica
    między "Pawłem" i "Gawłem" - dwa różne imiona, choć brzmią i wyglądają
    podobnie.
    
    Natomiast jeśli w treści błędu zobaczysz ``SyntaxError`` (błąd składni),
    oznacza to po prostu, że podany kod jest niezrozumiały dla MicroPythona. 
    Sprawdź czy nie brakuje żadnych znaków specjalnych, jak ``"`` czy ``:``. 
    To tak jak gdyby umieścić. kropkę w środku zdania. Trudno jest wtedy 
    zrozumieć co autor miał na myśli.
    
    Twój microbit może przestać reagować: nie uda się zaprogramować nowego
    kodu lub wpisywać poleceń w konsoli REPL. W takim przypadku spróbuj
    odłączyć urządzenie od prądu i podłączyć ponownie po krótkiej chwili.
    Chodzi o to, by odłączyć kabel USB (i kabel baterii jeśli jest podłączony),
    a po chwili podłączyć ponownie. Może być także konieczne zrestartowanie
    edytora kodu.
