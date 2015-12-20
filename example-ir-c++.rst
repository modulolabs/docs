.. _example-ir-c++:

IR Remote Example (C++)
---------------------------------------------

In this tutorial, we'll use use the IR Remote modulo to receive a signal from
a remote control and toggle the controller's builtin LED.

Hardware required:

* Modulo Base (or Modulo Particle Base)
* Controller Modulo (or Particle Photon)
* IR Remote Modulo

The following example requires the Modulo arduino library v1.0 or later. For
particle, it requires the Modulo library v1.2.0 or greater.

Run this program in the Arduino app by going to the "Arduino > Examples > Modulo"
menu and selecting "IRTutorial". If you're working with particle, look for
IRTUTORIAL.ino in the Modulo library.

.. code-block:: c++

    #include "Modulo/Modulo.h"


    #ifdef PARTICLE
    #define LED_BUILTIN 7
    #endif

    IRRemoteModulo ir;

    // The following codes are for the SparkFun Remote Control,
    // which uses the NEC protocol.
    //    https://www.sparkfun.com/products/11759
    #define BUTTON_UP 0x10EFA05F
    #define BUTTON_DOWN 0x10EF00FF
    #define BUTTON_LEFT 0x10EF10EF
    #define BUTTON_RIGHT 0x10EF807F
    #define BUTTON_CENTER 0x10EF20DF
    #define BUTTON_A 0x10EFF807
    #define BUTTON_B 0x10EF7887
    #define BUTTON_C 0x10EF58A7
    #define BUTTON_POWER 0x10EFD827

    // The current state of the led
    bool ledState = false;

    // This callback funtion is registered with the IRRemoteModulo object so that it
    // runs anytime a new IR code is received.
    void irReceiveCallback(int8_t protocol, uint32_t code, uint16_t *rawData, uint8_t rawLen) {
        // Print the protocol, code, and raw data to the Serial port
        // This makes it easy to make capturing codes for other remotes
        // by just opening the serial monitor in the Arduino app.
        Serial.print("Received: (");
        Serial.print(protocol);
        Serial.print(",0x");
        Serial.print(code, HEX);
        Serial.print(") rawData[");
        Serial.print(rawLen);
        Serial.print("] = {");
        for (int i=0; i < rawLen; i++) {
            Serial.print(rawData[i]);
            if (i != rawLen-1) {
                Serial.print(",");
            }
        }
        Serial.println("}");

        // Toggle the LED when the center button is pressed
        if (protocol == IR_PROTOCOL_NEC and code == BUTTON_CENTER) {
            ledState = !ledState;
        }
        digitalWrite(LED_BUILTIN, ledState);
    }

    void setup() {
        Serial.begin(9600);
        ir.setReceiveCallback(&irReceiveCallback);

        // Configure the builtin LED as an output
        pinMode(LED_BUILTIN, OUTPUT);
    }

    void loop() {
        Modulo.loop();
    }
