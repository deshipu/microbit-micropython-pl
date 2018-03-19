Wejście/Wyjście
---------------

Na dolnej krawędzi micro:bita znajdują się paski metalu, które sprawiają, że urządzenie wygląda
jakby miało zęby. Są to piny wejścia/wyjścia, w skrócie piny we/wy (ang. input/output - I/O).

.. image:: blue-microbit.png

Niektóre piny są większe od innych, aby było możliwe podłączenie do nich krokodylków (zacisków). 
Są one oznaczone 0, 1, 2, 3V oraz GND (komputery zawsze zaczynają liczyć od zera). Jeśli podłączysz
płytkę złącza krawędziowego do urządzenia, będziesz mógł podłączać kabelki również do pozostałych 
(mniejszych) pinów.

Każdy pin micro:bita jest reprezentowany przez *obiekt* o nazwie ``pinN``, gdzie ``N`` jest numerem pinu.
Zatem, na przykład, aby zrobić coś z pinem oznaczonym numerem 0 (zero) użyj obiektu o nazwie ``pin0``.

Proste!

Te obiekty posiadają różne *metody*, w zależności od tego, do czego dany pin może zostać wykorzystany.

Delikatny Python
++++++++++++++++

Najprostszym przykładem wejścia przez pin jest sprawdzenie, czy jest on dotknięty. 
W taki oto sposób możesz połaskotać swoje urządzenie, aby je rozśmieszyć::

    from microbit import *

    while True:
        if pin0.is_touched():
            display.show(Image.HAPPY)
        else:
            display.show(Image.SAD)

Jedną ręką trzymaj urządzenie za pin GND. Następnie, drugą ręką dotknij (lub połaskocz) 
pin 0 (zero). Powinieneś zobaczyć na wyświetlaczu zmianę z miny smutnej na szczęśliwą!

To jest tylko bardzo podstawowa forma sprawdzenia działania wejścia. Prawdziwa zabawa
zaczyna się, gdy do pinów podłączysz obwody oraz inne urządzenia.

Piski i buczenia
++++++++++++++++

Najprostszą rzeczą, które możemy podłączyć do naszego urządzenia
jest brzęczyk piezoelektryczny. Użyjemy go jako wyjście.

.. image:: piezo_buzzer.jpg

To małe urządzenie wydaje wysoki dźwięk, kiedy zostanie podłączone do obwodu. Aby podłączyć 
je do swojego micro:bita, możesz przypiąć krokodylki do pinu 0 oraz GND
(jak widać na poniższym obrazku).

.. image:: pin0-gnd.png

Kabel z pinu 0 powinien być podłączony do dodatniego złącza brzęczyka, a kabel z pinu GND 
do złącza ujemnego.

Poniższy program sprawi, że brzęczyk wyda dźwięk::

    from microbit import *

    pin0.write_digital(1)

Jest to zabawne przez około 5 sekund, ale potem będziesz chciał wyłączyć ten okropny dźwięk.
Rozbudujmy nasz przykład i sprawmy, aby urządzenie wydawało piski::

    from microbit import *

    while True:
        pin0.write_digital(1)
        sleep(20)
        pin0.write_digital(0)
        sleep(480)

Czy domyślasz się jak działa ten skrypt? Pamiętaj, że w cyfrowym świecie ``1`` oznacza "włączony", 
zaś ``0`` "wyłączony".

Urządzenie jest wprowadzane w nieskończoną pętlę i natychmiast włącza pin 0. To powoduje,
że brzęczyk wydaje pisk. Podczas gdy brzęczyk piszczy, urządzenie usypia na 20 milisekund,
a następnie wyłącza pin 0. Daje to efekt krótkiego pisku. W końcu, urządzenie usypia 
na 480 milisekund, zanim rozpocznie pętlę od początku. To znaczy, że usłyszysz
dwa piski na sekundę (jeden co 500 milisekund).

Stworzyliśmy bardzo prosty metronom!

.. footer:: Obrazek brzęczyka piezoelektrycznego na licencji CC BY-NC-SA 3.0 z https://www.flickr.com/photos/tronixstuff/4821350094
