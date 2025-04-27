# ⭐ Zdalnie Sterowany Robot (C, STM32)

![GitHub stars](https://img.shields.io/github/stars/szymon-tulodziecki/stm32g070-rc-robot)
![C](https://img.shields.io/badge/C-00599C?style=flat&logo=c&logoColor=white)
![STM32](https://img.shields.io/badge/STM32-03234B?style=flat&logo=stmicroelectronics&logoColor=white)

Zdalnie sterowany robot oparty na mikrokontrolerze **STM32G070RB** z czujnikiem **HC-SR04** oraz komunikacją **Bluetooth**.

> ⚠️ **Uwaga:** Nie podłączaj baterii do mikrokontrolera bez zmiany ustawień zworki! <br>
> Domyślnie zworka jest ustawiona w pozycji ST-LINK, co oznacza, że mikrokontroler jest zasilany przez port Micro USB. Baterie podłącz na końcu, gdy cały projekt będzie gotowy. Następnie przełóż zworkę na pozycję VIN, co pozwoli zasilić mikrokontroler napięciem do 12 V. W przeciwnym razie możesz uszkodzić płytkę! <br>
> ⚠️

<div align="center">
  <img src="img/warning.png" alt="Schemat Połączeń 1" width="70%">
</div>

## 📦 1. Podzespoły

- 🛞 **Chassis Rectangle 2WD** – 2-kołowe podwozie robota z napędem
- 📦 **Nucleo-G070RB** – zestaw startowy z mikrokontrolerem STM32G070RB
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

#### Wybierz mikrokontroler STM32G070RB i opcję "NUCLEO"

<div align="center">
  <img src="img/img3.png" alt="Konfiguracja STM32G070RB" width="70%">
</div>

#### Nazwij swój projekt i utwórz go

<div align="center">
  <img src="img/img4.png" alt="Tworzenie projektu" width="70%">
</div>

---

### 📌 3.2 Schemat i konfiguracja pinów

<div align="center">
  <img src="img/img5.png" alt="Schemat pinów STM32G070RB" width="70%">
</div>

#### Skonfiguruj GPIO jako `GPIO_Output`, zgodnie ze schematem, i nadaj im odpowiednie nazwy: 

<div align="center">
  <img src="img/img6.png" alt="Piny GPIO_Output" width="70%">
</div>

#### Wyszukaj "USART2" i włącz go w trybie asynchronicznym, ustawiając Baud Rate na 9600:

<div align="center">
  <img src="img/img7.PNG" alt="USART" width="70%">
</div>

#### Przejdź do zakładki "NVIC Setting" i włącz przerwania:

<div align="center">
  <img src="img/img8.PNG" alt="USART" width="70%">
</div>

#### W sekcji Timers dla timera 1 ustaw PWM Generation CH1 dla Channel 1 oraz PWM Generation CH2 dla Channel 2:

<div align="center">
  <img src="img/img9.PNG" alt="Sterowanie" width="70%">
</div>

#### Ustaw wartość Prescaler na 16, a Counter Period na 999:

<div align="center">
  <img src="img/img10.PNG" alt="Sterowanie" width="70%">
</div>

#### Przejdź do timera 2 i ustaw Channel 3 w trybie Input Capture Direct Mode:

<div align="center">
  <img src="img/img11.PNG" alt="Czujnik" width="70%">
</div>

#### Ustaw Prescaler na 16:

<div align="center">
  <img src="img/img12.PNG" alt="Czujnik" width="70%">
</div>

#### Pin PB3 ustaw w trybie `GPIO_Output` i nadaj mu nazwę `TRIG`, a pinu PB10 (Channel 2 timera 2) nazwę `ECHO`:

<div align="center">
  <img src="img/img13.PNG" alt="Czujnik" width="70%">
</div>