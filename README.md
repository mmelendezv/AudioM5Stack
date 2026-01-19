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

Ya instalado el hardware en la Cardputer, se requiere lo siguiente
* Agregar los componentes:
   M5Unified
   M5GFX
   M5Unit-AudioPlayer: unit_audioplayer.cpp, unit_audioplayer.hpp
* Inicializar la unidad de audio con audioplayer.begin()

El codigo minimo para reproducir es el siguiente:


Click Upload ➡️


