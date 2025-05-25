# ⭐ Zdalnie Sterowany Robot (C, STM32)
![GitHub stars](https://img.shields.io/github/stars/szymon-tulodziecki/stm32g071-rc-robot?style=flat)
![C](https://img.shields.io/badge/C-00599C?style=flat&logo=c&logoColor=white)
![STM32](https://img.shields.io/badge/STM32-03234B?style=flat&logo=stmicroelectronics&logoColor=white)

Zdalnie sterowany robot oparty na mikrokontrolerze **STM32G071RB** z czujnikiem **HC-SR04** oraz komunikacją **Bluetooth**.

> ⚠️ **Uwaga:** Nie podłączaj baterii do mikrokontrolera bez zmiany ustawień zworki! <br>
> Domyślnie zworka jest ustawiona w pozycji ST-LINK, co oznacza, że mikrokontroler jest zasilany przez port Micro USB. Baterie podłącz na końcu, gdy cały projekt będzie gotowy. Następnie przełóż zworkę na pozycję VIN, co pozwoli zasilić mikrokontroler napięciem do 12 V. W przeciwnym razie możesz uszkodzić płytkę! <br>
> ⚠️

<div align="center">
  <img src="img/warning.png" alt="Schemat Połączeń 1" width="70%">
</div>

## 📦 1. Podzespoły

- 🛞 **Podwozie własnego projektu** – góra i dół wycięte na laserze, połączone śrubami 10mm, a ścianki wydrukowane w 3D (Archiwum CircularChassis2WD)
https://github.com/szymon-tulodziecki/CircularChassis2WD

- 📦 **Nucleo-G071RB** – zestaw startowy z mikrokontrolerem STM32G071RB
- 📶 **Bluetooth HC-05** – moduł komunikacji bezprzewodowej
- ⚙️ **L293D** – 2-kanałowy sterownik silników
- 📏 **HC-SR04** – ultradźwiękowy czujnik odległości
- 🔋 **Ogniwa 18650 (x3)** – akumulatory zasilające
- 🧰 **Koszyk na ogniwa 18650 (szeregowy)** – uchwyt na baterie
- 🔌 **Przewody M-F 17 cm** – przewody połączeniowe
- 🔩 **Zestaw śrub i tulei M3** – do montażu mechanicznego
- 🧪 **Płytka stykowa (170 pól)** – do prototypowania połączeń

---

## 🔌 2. Schemat Połączeń

<div align="center">
  <img src="img/img1.png" alt="Schemat Połączeń 1" width="70%">
</div>

<div align="center">
  <img src="img/img2.png" alt="Schemat Połączeń 2" width="70%">
</div>

---

## 🛠️ 3. Konfiguracja projektu STM32CubeIDE

> W tej sekcji przedstawiona jest pełna konfiguracja środowiska **STM32CubeIDE**, w tym tworzenie projektu, ustawienia pinów, timerów oraz komunikacji przez USART.

---

### ⚙️ 3.1 Tworzenie projektu

#### Wybierz mikrokontroler STM32G071RB i opcję "NUCLEO"

<div align="center">
  <img src="img/img3.PNG" alt="Konfiguracja STM32G071RB" width="70%">
</div>

#### Nazwij swój projekt i utwórz go

<div align="center">
  <img src="img/img4.png" alt="Tworzenie projektu" width="70%">
</div>

---

### 📌 3.2 Konfiguracja pinów oraz ustawień projektu:

<div align="center">
  <img src="img/img5.png" alt="Schemat pinów STM32G071RB" width="70%">
</div>

#### Skonfiguruj piny PA0, PA1, PA4, PA5 jako `GPIO_Output`, zgodnie ze schematem, i nadaj im odpowiednie nazwy (IN1, IN2, IN3, IN4): 

<div align="center">
  <img src="img/img6.PNG" alt="Piny GPIO_Output" width="70%">
</div>

#### Wyszukaj "USART2" i włącz go w trybie asynchronicznym, ustawiając Baud Rate na 9600:

<div align="center">
  <img src="img/img7.PNG" alt="USART" width="70%">
</div>

#### Przejdź do zakładki "NVIC Setting" i włącz przerwania:

<div align="center">
  <img src="img/img8.PNG" alt="USART" width="70%">
</div>

> Włączenie USART2 automatycznie skonfiguruje odpowiednie porty i nada im nazwy

#### W sekcji Timers dla timera 1 ustaw PWM Generation CH1 dla Channel 1 oraz PWM Generation CH2 dla Channel 2:

<div align="center">
  <img src="img/img9.PNG" alt="Sterowanie" width="70%">
</div>

#### Ustaw wartość Prescaler na 16, a Counter Period na 999:

<div align="center">
  <img src="img/img10.PNG" alt="Sterowanie" width="70%">
</div>

> Włączenie kanałów na Timerze automatycznie skonfiguruje odpowiednie porty i nada im nazwy

#### Przejdź do timera 2 i ustaw Channel 2 w trybie Input Capture Direct Mode:

<div align="center">
  <img src="img/img11.PNG" alt="Czujnik" width="70%">
</div>

#### Ustaw Prescaler na 16:

<div align="center">
  <img src="img/img12.PNG" alt="Czujnik" width="70%">
</div>

> Analogicznie dla timera 2 ustawienie jego kanału nada mu nazwę ale tym razem dla wygody zmienimy ją (kolejny krok)

#### Pin PB3 ustaw w trybie `GPIO_Output` i nadaj mu nazwę `TRIG`, a pinu PB10 (Channel 2 timera 2) nazwę `ECHO`:

<div align="center">
  <img src="img/img13.PNG" alt="Czujnik" width="70%">
</div>

#### Włącz przerwania dla Timera 2:

<div align="center">
  <img src="img/img14.jpeg" alt="Czujnik" width="70%">
</div>

---
### 📁 4. Zapisz projekt i wygeneruj kod

1. **Zapisz projekt** w STM32CubeIDE, akceptując generowanie kodu.
2. **Wklej kod z załącznika** do funkcji `main`.
3. **Podłącz płytkę Nucleo** do komputera, skompiluj projekt i wgraj go na mikrokontroler.
4. **Odłącz kabel USB**, przełóż zworkę na pozycję VIN i podłącz baterię zgodnie ze schematem.

#### 🧑‍💻 Kluczowe funkcje kodu (C, HAL):

- Sterowanie mostkiem H (jazda do przodu/do tyłu, skręcanie, zatrzymanie)
- Obsługa czujnika HC-SR04 (generowanie sygnału trigger, pomiar czasu echa, obliczanie odległości)
- Odbiór komend przez UART (Bluetooth), wywoływanie funkcji ruchu oraz zmiana prędkości przez PWM

---

### 📱 5. Aplikacja sterująca

> Do sterowania robotem służy dedykowana aplikacja, komunikująca się z modułem Bluetooth HC-05, działająca na systemach Windows.

Aplikację możesz pobrać z repozytorium GitHub:  
[https://github.com/szymon-tulodziecki/rcar-control-app](https://github.com/szymon-tulodziecki/rcar-control-app)

<div align="center">
  <img src="img/app.PNG" alt="Aplikacja Sterująca">
</div>
---

## 📝 Podsumowanie

Projekt przedstawia kompletny system zdalnie sterowanego robota opartego na STM32, wyposażonego w czujnik odległości oraz komunikację Bluetooth. W dokumentacji znajdziesz szczegółowe instrukcje dotyczące montażu, konfiguracji sprzętu i oprogramowania, a także gotową aplikację do sterowania robotem.  
Całość stanowi świetny punkt wyjścia do nauki programowania mikrokontrolerów, obsługi peryferiów oraz budowy własnych projektów robotycznych.

Zachęcam do rozwijania projektu i dzielenia się swoimi pomysłami!