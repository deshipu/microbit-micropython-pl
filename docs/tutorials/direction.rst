Kierunek
--------

Na urządzeniu BBC micro:bit znajduje się kompas. Jeżeli kiedykolwiek zrobisz
stację pogodową, możesz użyć micro:bita do sprawdzania kierunku wiatru.

Kompas
++++++

Urządzenie może również wskazać kierunek północny::

    from microbit import *

    compass.calibrate()

    while True:
        needle = ((15 - compass.heading()) // 30) % 12
        display.show(Image.ALL_CLOCKS[needle])

.. note:: 

    **Przed dokonaniem pomiaru należy skalibrować urządzenie.** W innym wypadku
    rezultaty będą niepoprawne. Aby urządzenie zorientowało się w swoim ustawieniu
    względem pola magnetycznego Ziemi, metoda ``calibration`` uruchamia małą,
    śmieszną grę. 

    Aby skalibrować kompas, obracaj micro:bitem, dopóki krańcowe piksele
    wyświetlacza nie utworzą koła.

Program używa ``compass.heading`` i, wraz z prostą, acz piękną matematyką,
`podłogą i sufitem <https://pl.wikipedia.org/wiki/Pod%C5%82oga_i_sufit>`_ ``//`` oraz `resztą z dzielenia <https://pl.wikipedia.org/wiki/Modulo>`_ ``%``, wyprowadza pozycję wskazówki zegara, po czym wyświetla ją tak,
by pokazywała mniej więcej północ.
