```c++
#include <TFT_eSPI.h>
#include <SPI.h>

TFT_eSPI tft = TFT_eSPI();       // TFT instance
TFT_eSPI_Button btn;             // Button instance

void setup() {
  tft.init();
  tft.setRotation(1);
  tft.fillScreen(TFT_BLACK);

  // Initialize and draw the button
  btn.initButton(&tft, 120, 100, 100, 40, TFT_WHITE, TFT_RED, TFT_WHITE, "Click", 2);
  btn.drawButton();
}

void loop() {
  uint16_t x = 0, y = 0;    // Variables to store touch coordinates

  // Check for touch
  if (tft.getTouch(&x, &y)) {
    if (btn.contains(x, y)) {
      tft.fillScreen(TFT_GREEN);
      delay(500);
      tft.fillScreen(TFT_BLACK);
      btn.drawButton();
    }
  }

  delay(50); // Small delay to debounce
}
```

In this example, we begin by initializing the screen with a black background. We then create a
[`TFT_eSPI_Button`](class.md) object named btn, which is configured and drawn in the `setup()` function using the
[`drawButton()`](drawbutton.md) method.

Inside the `loop()` function, we detect touch input using the getTouch() method, which returns the coordinates of the
touch point. These coordinates are passed to the [`contains()`](contains.md) method to check whether the touch occurred
within the button's boundaries. If the button is pressed, we perform an action—in this case, filling the screen with
green to indicate a successful press, then restoring the button display.

!!! Note
    This example assumes you have a touchscreen properly connected to your ESP32 or ESP8266 board, and that the
    `TFT_eSPI` library has been correctly configured for your specific display and touch controller.
