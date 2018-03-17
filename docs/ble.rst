Bluetooth
*********

Wprawdzie BBC micro:bit jest wyposażony w sprzęt pozwalający na pracę jako
urządzenie Bluetooth Low Energy (BLE), ma jednak tylko 16 kilobajtów pamięci
RAM. Oprogramowanie BLE zajmuje 12 kilobajtów pamięci RAM, przez co nie zostaje
jej wystarczająco dużo na MicroPythona.

Jest możliwe, że przyszłe wersje urządzenia będą wyposażone w 32 kilobajty
pamięci RAM, co może już wystarczyć. Dopóki to nie nastąpi, wsparcie dla BLE
w MicroPythonie jest mało prawdopodobne.

.. note::
    MicroPython daje dostęp do wbudowanego radia poprzez moduł ``radio``.
    Pozwala to użytkownikom na stworzenie prostej, lecz efektywnej
    bezprzewodowej sieci urządzeń micro:bit.

    Ponadto, protokół używany w module ``radio`` jest znacznie prostszy niż
    BLE. Jest dzięki temu łatwiejszy w użyciu w edukacji.
