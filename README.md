# AudioM5Stack
Modulo de Audio para M5Stack para Cardputer

![20260108_205630](https://github.com/user-attachments/assets/0860cb92-1396-4d51-bdca-b4515894ec18)

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

```
#include <M5Unified.h>
#include <M5GFX.h>
#include <unit_audioplayer.hpp>
AudioPlayerUnit audioplayer;
void setup()
{
    auto cfg            = M5.config();
    cfg.serial_baudrate = 115200;
    M5.begin(cfg);
    M5.Power.setExtOutput(true);
    M5.Lcd.fillScreen(WHITE);
    M5.Lcd.setTextFont(&fonts::DejaVu18);
    M5.Lcd.setTextColor(TFT_BLACK);
    M5.Display.drawString("Unidad AudioPlayer Demo", 0, 0);

    int8_t port_a_pin1 = -1, port_a_pin2 = -1;
    port_a_pin1 = M5.getPin(m5::pin_name_t::port_a_pin1);
    port_a_pin2 = M5.getPin(m5::pin_name_t::port_a_pin2);
    Serial.printf("getPin: RX:%d TX:%d\n", port_a_pin1, port_a_pin2);
    //To change the serial port, please modify this section.
    while (!audioplayer.begin(&Serial1, port_a_pin1, port_a_pin2)) {//Default UART Num: 1,
        delay(1000);
    }
    Serial.println("Unidad AudioPlayer lista");
    audioplayer.setPlayMode(AUDIO_PLAYER_MODE_SINGLE_STOP);//Default Play Mode: single stop
    audioplayer.playAudio();
    audioplayer.selectAudioNum(1);//Default Audio Num: 1
    M5.Display.drawString("Audio Num:1", 0, 80);
    audioplayer.setVolume(25);
}

void loop()
{
    static uint8_t lastPlayStatus = 255;
    static uint8_t lastAudioNum = 0, lastVolume = 0;
    static bool refreshAudioNum = false;
    uint8_t playStatus = audioplayer.checkPlayStatus();
    uint8_t volume     = audioplayer.getVolume();
    uint8_t audioNum   = 0;
    if (refreshAudioNum) {
        audioNum        = audioplayer.getCurrentAudioNumber();
        refreshAudioNum = false;
    } else {
        audioNum = lastAudioNum;
    }
    if (playStatus != lastPlayStatus) {
        static String playStatusStr;
        if (playStatus == AUDIO_PLAYER_STATUS_PAUSED) {
            playStatusStr = "Paused";
        } else if (playStatus == AUDIO_PLAYER_STATUS_STOPPED) {
            playStatusStr = "Stopped";
        } else if (playStatus == AUDIO_PLAYER_STATUS_PLAYING) {
            playStatusStr = "Playing";
        }
        M5.Display.fillRect(0, 40, 320, 20, WHITE);
        M5.Display.drawString("Play Status:" + playStatusStr, 0, 40);
        lastPlayStatus = playStatus;
    }

    if (volume != lastVolume) {
        M5.Display.fillRect(0, 120, 320, 20, WHITE);
        M5.Display.drawString("Volume:" + String(volume), 0, 120);
        lastVolume = volume;
    }

   if (audioNum != lastAudioNum && audioNum != AUDIO_PLAYER_STATUS_ERROR) {
        M5.Display.fillRect(0, 80, 320, 20, WHITE);
        M5.Display.drawString("Audio Num:" + String(audioNum), 0, 80);
        lastAudioNum = audioNum;
    }
    M5.update();
}
```
Algo mas elaborado y llamativo es la siguiente aplicacion 

https://github.com/AndyAiCardputer/unit_audio-player-cardputer



