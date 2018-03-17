Radio
*****

.. py:module:: radio

Moduł "radio" umożliwia urządzeniom wspólną pracę przez prostą sieć bezprzewodową.  

Moduł radia z zamyśle jest bardzo prosty:

* Przesyłane wiadomości są konfigurowanej długości (do 251 bajtów). 
* Otrzymywane wiadomości przechowywane są w kolejce o określonej konfigurowalnej wielkości (im większa kolejka tym większe zużycie pamięci RAM). Jeżeli kolejka jest pełna, nowa wiadomość przychodząca zostanie zignorowana. 
* Wiadomości przesyłane są wcześniej wybranym kanałem (zakres numeracji 0-100).
* Nadawanie z określoną mocą sygnału - im większa moc, tym większy zasięg nadawania. 
* Wiadomości filtrowane są według adresów (jak numery domów) i grup (jak nazwisko adresata pod danym adresem).
* Przepustowość może być na jednym z trzech predefiniowanych ustawień.  
* Wysyłanie i odbierania danych różnych typów.
* Dodatkowym ułatwieniem dla dzieci są łatwe do wysyłania i odbierania wiadomości w postaci ciągów znaków. 
* Domyślna konfiguracja jest rozsądna i kompatybilna z innymi platformami związanymi z BBC micro:bit.
	
Aby mieć dostęp do tego modułu musisz wykonać import: 	

	import radio

Zakładamy, że już to zrobiłeś dla poniższych przykładów. 

Stałe
=====

.. py:attribute:: RATE_250KBIT

    Stała oznaczająca przepustowość 256 Kbit na sekundę. 

.. py:attribute:: RATE_1MBIT

    Stała oznaczająca przepustowość 1 MBit na sekundę. 

.. py:attribute:: RATE_2MBIT

    Stała oznaczająca przepustowość 2 MBit na sekundę. 


Funkcje
=======

.. py:function:: on()

	Włącza radio. Funkcja musi być wywołana świadomie ponieważ radio pobiera prąd i zajmuje zasoby pamięci, które mogą być potrzebne do czegoś innego.  

.. py:function:: off()

	Wyłącza radio oszczędzając prąd i pamięć. 

.. py:function:: config(**kwargs)

	Konfiguruje ustawienia związane z radiem. Nazwy ustawień oparte są o słowa kluczowe.
	Dostępne ustawienia i ich rozsądne domyślne wartości są podane poniżej.
	
	``length`` - długość (wartość domyślna = 32) definiuje maksymalną długość, w bajtach, wiadomości przesyłanej przez radio. Może mieć do 251 bajtów długości (254 - 3 bajty dla S0, długości i preambuły S1). 
	
	``queue`` - kolejka (wartość domyślna = 3) określa liczbę wiadomości, które mogą być przechowywane w kolejce wiadomości przychodzących. Jeżeli nie ma wolnego miejsca w kolejce, następna wiadomość przychodząca zostanie pominięta. 
	
	``channel`` - kanał (wartość domyślna = 7) musi być liczbą całkowitą od 0 do 100 (włącznie), która określa kanał na który nastrojone jest radio. Wiadomości będą wysyłane tym kanałem i tylko wiadomości otrzymane tym kanałem będą umieszczone w kolejce wiadomości przychodzących. Każdy kanał ma szerokość 1MHz, począwszy od 2400MHz. 
	
	``power`` - moc (domyślna wartość = 6) jest liczbą całkowitą od 0 do 7 (włącznie) służącą do wskazania mocy sygnału w czasie nadawania. Im wyższa liczba tym mocniejszy sygnał, ale też większe zużycie prądu przez urządzenie. Wartości stałej odwołują się do poszczególnych wartości mocy nadawania wyrażonej w decybelach miliwatów [dbm]: -30, -20, -16, -12, -8, -4, 0, 4.

	``address`` - adres (domyślna wartość = 0x75626974) to ustalona nazwa, wyrażona jako 32 bitowy adres, stosowana do filtrowania przychodzących pakietów na poziomie sprzętowym, zachowując tylko pasujące do ustawionego adresu. Wartość domyślna jest również stosowana domyślnie na innych platformach kompatybilnych z micro:bit.
	
	``group`` - grupa (domyślna wartość = 0) jest 8 bitową wartością (0-255) stosowaną razem z adresem, do filtrowania wiadomości. Dla lepszego zobrazowania "adres" jest jak adres domu a "grupa" jest jak osoba w nim mieszkająca do której adresujemy przesyłkę.

	``data_rate`` - (domyślne ustawienie = radio.RATE_1MBIT) wyraża prędkość przesyłu danych. Może przyjmować jedną ze stałych zdefiniowanych w module "radio": ``RATE_250KBIT``, ``RATE_1MBIT`` lub ``RATE_2MBIT``.

	Jeżeli "config" nie zostanie wywołany wtedy przyjęte zostaną ustawienia o domyślnych wartościach. 

.. py:function:: reset()

	Zresetuj ustawienia do wartości domyślnych (patrz powyżej w dokumentacji funkcji config). 

.. note::

	Żadna z powyższych metod wysyłania lub nadawania nie będzie działać jeżeli radio nie będzie włączone. 

.. py:function:: send_bytes(treść wiadomości)

	Wysyła wiadomość składającą się z bajtów.

.. py:function:: receive_bytes()

	Wczytuje z kolejki pierwszą wiadomość przychodzącą. Zwraca "None" (brak) jeżeli nie ma oczekujących wiadomości. Wiadomości wyświetlane są jako bajty. 
	
.. py:function:: receive_bytes_into(buffer)

	Odbiera następną wiadomość przychodzącą z kolejki wiadomości. Kopiuje treść wiadomości do bufora, ucinając jej koniec jeśli to konieczne. Zwraca "None" jeżeli nie ma wiadomości oczekujących, jeżeli są, zwraca długość wiadomości (długość wiadomości może być dłuższa od długości bufora). 

.. py:function:: send("treść wiadomości")

	Wysyła wiadomość w postaci ciągu znaków. Jest odpowiednikiem ``send_bytes(bytes(treść wiadomości, 'utf8'))``, ale z ``b'\x01\x00\x01'`` dodanymi na początku (dla zapewnienia kompatybilności z innymi platformami współpracującymi z micro:bit).

.. py:function:: receive()

	Funkcja działa dokładnie w ten sam sposób co ``receive_bytes`` przy czym zwraca wiadomość w takiej postaci w jakiej była wysyłana.
	
	Obecnie jest to odpowiednik ``str(receive_bytes(), 'utf8')``, ale ze sprawdzeniem czy pierwsze 3 bajty to ``b'\x01\x00\x01'`` (dla zapewnienia kompatybilności z innymi platformami współpracującymi z micro:bit). Te trzy bajty są usuwane przed konwersją na ciąg znaków. 

    
	Wyjątek ``ValueError`` wyświetlany jest w przypadku niepowodzenia konwersji treści wiadomości na ciąg znaków.

Przykłady 
---------

.. include:: ../examples/radio.py
    :code: python
