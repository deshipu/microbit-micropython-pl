Gesty
--------

Naprawdę interesującym efektem ubocznym posiadania akcelerometru jest wykrywanie gestów. 
Jeśli poruszysz swoim micro:bitem w pewien specjalny sposób (jak przy wykonywaniu gestu), 
MicroPython jest w stanie to wykryć.

MicroPython potrafi rozpoznać następujące gesty: ``up`` (ang. w górę), ``down`` (ang. w dół),
``left`` (ang. w lewo), ``right`` (ang. w prawo), ``face up`` (ang. zwrócony w górę), 
``face down`` (ang. zwrócony w dół), ``freefall`` (ang. swobodne spadanie), ``3g``, ``6g``,
``8g``, ``shake`` (ang. potrząśnięcie). Gesty zawsze są reprezentowane przez ciągi znaków.
Podczas gdy większość z tych nazw powinna być oczywista, gesty ``3g``, ``6g`` oraz ``8g``
odnoszą się do sytuacji, w której na urządzenie oddziałują odpowiadające poziomy przeciążenia 
(jak na astronautę, kiedy jest wystrzeliwany w kosmos).

Aby pobrać aktualny gest użyj metody ``accelerometer.current_gesture``.
Jej wynikiem będzie jeden z nazwanych gestów z powyższej listy. Na przykład,
ten program sprawi, że Twoje urządzenie będzie szczęśliwe tylko, 
kiedy będzie zwrócone ku górze::

    from microbit import *

    while True:
        gesture = accelerometer.current_gesture()
        if gesture == "face up":
            display.show(Image.HAPPY)
        else:
            display.show(Image.ANGRY)

Ponieważ chcemy, aby urządzenie reagowało na zmieniające się okoliczności,
używamy pętli ``while``. Wewnątrz pętli aktualny gest jest odczytywany
i podstawiany pod zmienną ``gesture``. Warunek ``if`` sprawdza, czy ``gesture`` 
jest równa ``"face up"`` (Python używa ``==`` aby sprawdzić równość, pojedynczy
znak równości ``=`` jest używany do przypisywania - tak samo jak przypisujemy 
odczyt gestu do objektu ``gesture``). Jeżeli ``gesture`` jest równa ``"face up"``,
używamy wyświetlacza do pokazania szczęśliwej miny. W przeciwnym przypadku, 
urządzenie wyświetli rozzłoszczoną minę.

Magic-8
+++++++

Magiczna bila 8 to zabawka wynaleziona w latach pięćdziesiątych. Pomysł polega na zadaniu 
pytania typu tak lub nie, potrząśnięciu bilą i poczekaniu, aż wyjawi prawdę. Raczej
łatwo jest napisać działający w taki sposób program::

    from microbit import *
    import random

    answers = [
        "To pewne",
        "Zdecydowanie tak",
        "Bez wątpienia",
        "Tak, z pewnością",
        "Możesz na tym polegać",
        "Jak ja to widzę, tak",
        "Najprawdopodobniej",
        "Wygląda dobrze",
        "Tak",
        "Znaki wskazują na tak",
        "Odpowiedź niejasna, spróbuj ponownie",
        "Zapytaj ponownie później",
        "Lepiej, abym teraz nie powiedziała",
        "Nie mogę teraz przewidzieć",
        "Skoncentruj się i zapytaj ponownie",
        "Nie licz na to",
        "Moja odpowiedź brzmi nie",
        "Moje źródła mówią nie",
        "Nie wygląda to dobrze",
        "Bardzo wątpliwe",
    ]

    while True:
        display.show("8")
        if accelerometer.was_gesture("shake"):
            display.clear()
            sleep(1000)
            display.scroll(random.choice(answers))

Większość programu to tablica nazwana ``answers`` (ang. odpowiedzi). 
Sama gra znajduje się w pętli ``while`` na końcu.

Domyślny stan gry wyświetla cyfrę ``"8"``. Jednak program musi wykryć, 
że nastąpiło potrząśnięcie. Metoda ``was_gesture`` używa swojego argumentu (w tym przypadku
ciągu ``"shake"``, ponieważ chcemy wykryć potrząśnięcie) i zwraca ``True`` lub ``False``.

Jeżeli urządzenie było potrząśnięte, warunek ``if`` wykonuje swój blok kodu, w którym 
czyści ekran, czeka przez sekundę (aby urządzenie wyglądało, jakby zastanawiało się nad 
twoim pytaniem), a następnie wyświetla losowo wybraną odpowiedź.

Nie masz wrażenia, że jest to najlepszy program na świecie? Co mógłbyś
zrobić, aby "oszukać" i uzyskać zawsze pozytywną lub negatywną odpowiedź? 
(Podpowiedź: użyj przycisków).

