# AudioM5Stack
Modulo de Audio para M5Stack para Cardputer

La unidad de AudioPlayer permite reproducir MP3 a través del decodificador de audio N9301, además cuenta con una ranura para tarjeta microSD.. La señal de audio se emite a través de un conector de 3.5 mm, lo que proporciona una salida de audio nítida. 
Esta unidad es apta para la Cardputer de M5Stack a través del conector I2C Grove.

Características:
 * Chip N9301 decodificador de audio.
 * Interface UART
 * Jack stereo 3.5mm.
 * Soporta MP3 y WAV
 * Soporta FAT16/FAT32 
 * Soporta hasta 32GB microSD 
 * Para desarrollo de Arduino/PlatforIO/UiFlow1/UiFlow2

Para Cardputer se requiere intstalar el IDE de Arduino o PlatformIO (cualquiera de las dos plataformas recomendadas). Con ello, este es el procedimiento:
1. Instalalar IDE de Arduino o PlatformIO
2. Agregar la placa de M5Stack board
Tools → Board Manager → Search "M5Stack"
Install M5Stack by M5Stack
Install libraries:
M5Unified
M5GFX
ESP8266Audio
Open src/audio_player_unit.ino
Select board: M5Stack Cardputer
Click Upload ➡️

