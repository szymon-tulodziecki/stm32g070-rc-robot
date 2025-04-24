# ⭐ Zdalnie Sterowany Robot (C, STM32)

![GitHub stars](https://img.shields.io/github/stars/szymon-tulodziecki/stm32g070-rc-robot)
![C](https://img.shields.io/badge/C-00599C?style=flat&logo=c&logoColor=white)
![STM32](https://img.shields.io/badge/STM32-03234B?style=flat&logo=stmicroelectronics&logoColor=white)

Zdalnie sterowany robot oparty na mikrokontrolerze STM32G070RB z czujnikiem HC-SR04 oraz komunikacją Bluetooth.

> **⚠️ Uwaga: Kroki wykonania są istotne, patrz punkt 4.**


## 1. Podzespoły

- Chassis Rectangle 2WD - 2-kołowe podwozie robota z napędem.

- Nucleo-G070RB - zestaw startowy z mikrokontrolerem STM32G070RB.

- Moduł Bluetooth HC-05 - Moduł do komunikacji bezprzewodowej.

- Moduł L293D - 2-kanałowy sterownik silnika - Sterownik do obsługi silników robota.

- Ultradźwiękowy czujnik odległości HC-SR04 - Czujnik do pomiaru odległości.

- Ogniwo 18650 - Akumulator do zasilania robota (3 sztuki).

- Koszyk na 3 akumulatory typu 18650 - Koszyk na akumulatory.

- Przewody połączeniowe M-F różnokolorowe 17 cm (40 szt.) - Przewody do połączeń elektrycznych.

- Zestaw nylonowych śrub i tulei M3.

- Płytka stykowa biała 170 pól prototypowa - Płytka do prototypowania połączeń.


## 2. Schemat Połączeń

![Schemat Połączeń 1](img/img1.png)

![Schemat Połączeń 2](img/img2.png)


## 3. Konfiguracja projektu STM32CubeIDE


> W tej części przedstawiona jest cała konfiguracja środowiska STM32CubeIDE, łącznie z tworzeniem projektu, ustawianiem pinów, timerów oraz komunikacji USART. 
-------------------------------------------------
## 3.1 Tworzenie projektu

### Wyszukujemy STM32G070RB oraz wybieramy opcje "NUCLEO"

![Konfiguracja 1](img/img3.png)

### Przechodzimy dalej, nadajemy nazwę swojemu projektowi i go tworzymy

![Konfiguracja 2](img/img4.png)

### 3.2 Schemat pinów STM32G070RB

![Konfiguracja ](img/img5.png)

### 3.2 Konfiguracja pinów GPIO_OUTPUT 

