Wprowadzenie
------------

Zalecamy używanie `edytora Mu <http://codewith.mu/>`_ podczas pracy z tym
poradnikiem. Instrukcje dotyczące ściągnięcia i instalacji Mu znajdują się na
jego stronie internetowej. Może być też konieczne zainstalowanie sterownika, w
zależności od platformy (szczegółowe instrukcje na stronie).

Mu działa na Windowsie, OSX i na Linuksie.

Kiedy już zainstalujesz Mu, uruchom go i podłącz swój micro:bit do komputera
przy pomocy kabla USB.

Napisz swój skrypt w oknie edytora i kliknij ikonkę "Flash" aby przesłać go do
micro:bita. Jeśli to nie zadziała, upewnij się, że micro:bit pojawia się w
eksploratorze plików jako dysk.

.. toctree::
    :maxdepth: 2
    :caption: Tutorials

    hello
    images
    buttons
    io
    music
    random
    movement
    gestures
    direction
    storage
    speech
    network
    radio
    next

Python jest jednym z `najpopularniejszych
<http://www.tiobe.com/index.php/content/paperinfo/tpci/index.html>`_ na świecie
języków programowania. Zapewne codziennie używasz oprogramowania napisanego w
Pythonie, nie zdając sobie nawet z tego sprawy. Wszelkiego rodzaju firmy i
organizacje używają Pythona do różnorodnych zastosowań. Google, NASA, Banki,
Disney, CERN, YouTube, Mozilla, Newspapers -- lista jest długa i obejmuje
wszystkie obszary handlu, nauki i sztuki.

Dla przykładu, pamiętasz ogłoszone niedawno `odkrycie fal grawitacyjnych
<http://www.bbc.co.uk/news/science-environment-35552207>`_? Instrumenty
pomiarowe użyte tam były sterowane za `pomocą Pythona
<https://www.reddit.com/r/IAmA/comments/45g8qu/we_are_the_ligo_scientific_collaboration_and_we/czxnlux>`_.

Po prostu, nauka Pythona da ci niesłychanie cenną umiejętność, która ma
zastosowanie we wszystkich obszarach ludzkich starań.

Jednym z takich obszarów jest zadziwiające urządzenie micro:bit, stworzone
przez BBC. Działa na nim wersja Pythona nazwana MicroPython, która jest
specjalnie zaprojektowana dla małych komputerów jak ten. Jest to pełnoprawna
implementacja Pythona 3, wiec tego samego języka, którego używać będziesz
później (na przykład do programowania Raspberry Pi).

MicroPython nie zawiera wszystkich bibliotek standardowych, które zawarte są w
"zwykłym" Pythonie, jednakże stworzyliśmy specjalnym moduł nazwany
``microbit``, który pozwala na pełną kontrolę nad micro:bit.

Zarówno Python, jak i MicroPython, to otwarte oprogramowanie. To znaczy nie
tylko to, że nie trzeba za nie płacić, ale także to, że każdy może dodać coś od
siebie do ich społeczności. To może być kod, dokumentacja, raporty o błędach,
lokalna grupa użytkowników, albo nowe poradniki (jak ten). W zasadzie wszystkie
materiały dotyczące BBC micro:bit zostały stworzone przez międzynarodowy zespół
ochotników, pracujących w swoim wolnym czasie.

Te oto lekcje wprowadzają do MicroPythona i BBC micro:bit w prostych krokach.
Mogą one być swobodnie wykorzystywane i modyfikowane do lekcji szkolnych.
Możesz też uczyć się z nich w domu.

Najwięcej zyskasz odkrywając, eksperymentując i bawiąc się. Nie da się zepsuć
BBC micro:bit pisząc i uruchamiając na nim błędy kod, więc po prostu spróbuj!

Słowo ostrzeżenia: nie wszystko uda się za pierwszym razem i nie ma w tym nic
złego. Porażki są najlepszym sposobem nauki dla dobrych programistów. Szukanie
błędów i unikanie powtarzania błędów jest źródłem dużej satysfakcji dla tych z
nas, którzy są programistami.

W razie wątpliwości, pamiętaj Zen MicroPythona::

    Koduj,
    Skleć to do kupy,
    Mniej to więcej,
    Upraszczaj,
    Małe jest piękne,

    Bądz dzielny! Psuj rzeczy! Ucz się i baw się dobrze!
    Wyraź siebie przez MicroPythona.

    Miłego hakowania! :-)

Powodzenia!
