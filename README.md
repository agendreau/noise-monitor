# Noise Monitor

## Introduction 
Now you will create a system to monitor the noise level in the classroom. You can use ``||music: speaker||`` to make a sound when there is a lot of sound. You can use the ``||neopixel: five LEDs||`` on the gator:bit or the ``||basic: LEDS||`` on the micro:bit. You will use the ``||logic: if then else||`` blocks to ask questions about the value of the ``||gatorMicrophone: sound||`` to decide what you want to do. Lastly don't forget to think about ``||basic: how often||`` you want to take measurements, how you will ``||input: control||`` when the measurements are taken, and ``||loops: how many||`` measurements you want to take. Two potential solutions are in the Hint. When you think you've got it, ``|Download|`` the code and try it out.

```blocks
input.onButtonPressed(Button.A, function () {
    for (let i = 0; i < 4; i++) {
        strip.clear()
        strip.show()
        basic.pause(10000)
        sound = gatorMicrophone.getSoundIntensity()
        if (sound < 500) {
            basic.showIcon(IconNames.Happy)
            music.playTone(262, music.beat(BeatFraction.Whole))
            music.rest(music.beat(BeatFraction.Whole))
            strip.setPixelColor(0, neopixel.colors(NeoPixelColors.Blue))
            strip.show()
        } else if (sound < 1000) {
            basic.showLeds(`
                . . . . .
                . # . # .
                . . . . .
                # . . . #
                . # # # .
                `)
            strip.setPixelColor(0, neopixel.colors(NeoPixelColors.Blue))
            strip.setPixelColor(1, neopixel.colors(NeoPixelColors.Green))
        } else if (sound < 1500) {
            basic.showLeds(`
                . . . . .
                . # . # .
                . . . . .
                . . . . .
                # # # # #
                `)
            strip.setPixelColor(0, neopixel.colors(NeoPixelColors.Blue))
            strip.setPixelColor(1, neopixel.colors(NeoPixelColors.Green))
            strip.setPixelColor(2, neopixel.colors(NeoPixelColors.Yellow))
        } else if (sound < 2000) {
            basic.showIcon(IconNames.Sad)
            strip.setPixelColor(0, neopixel.colors(NeoPixelColors.Blue))
            strip.setPixelColor(1, neopixel.colors(NeoPixelColors.Green))
            strip.setPixelColor(2, neopixel.colors(NeoPixelColors.Yellow))
            strip.setPixelColor(3, neopixel.colors(NeoPixelColors.Orange))
        } else {
            basic.showIcon(IconNames.Sad)
            strip.showColor(neopixel.colors(NeoPixelColors.Red))
            music.beginMelody(music.builtInMelody(Melodies.Wawawawaa), MelodyOptions.Once)
        }
        basic.pause(10000)
    }
})
let sound = 0
let strip: neopixel.Strip = null
strip = neopixel.create(DigitalPin.P12, 5, NeoPixelMode.RGB)
gatorMicrophone.setGain(GainOptions.Eight)
```

```package
gatorMicrophone=github:sparkfun/pxt-gator-microphone
neopixel=github:microsoft/pxt-neopixel
```







