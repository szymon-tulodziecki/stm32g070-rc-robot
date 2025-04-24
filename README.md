# ⭐ Zdalnie Sterowany Robot (C, STM32)

![GitHub stars](https://img.shields.io/github/stars/szymon-tulodziecki/stm32g070-rc-robot)
![C](https://img.shields.io/badge/C-00599C?style=flat&logo=c&logoColor=white)
![STM32](https://img.shields.io/badge/STM32-03234B?style=flat&logo=stmicroelectronics&logoColor=white)

Zdalnie sterowany robot oparty na mikrokontrolerze **STM32G070RB** z czujnikiem **HC-SR04** oraz komunikacją **Bluetooth**.

> ⚠️ **Uwaga:** Nie podłączaj baterii do mikrokontrolera bez zmiany ustawień zworki! <br>
> Natywnie zworka ustawiona jest na pozycji STLINK, co oznacza, że mikrokontroler zasilany jest przez port Micro USB. Baterie podłącz na koniec, gdy cały projekt będzie gotowy. Wtedy przełóż zworkę na pozycję VIN, co pozwoli na zasilenie mikrokontrolera z napięcia do 12V. Inaczej możesz uszkodzić swoją płytkę!
⚠️ 

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
- 🧰 **Koszyk na ogniwa 18650 szeregowy** – uchwyt na baterie
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

#### Konfiguracja GPIO jako `GPIO_Output`  
