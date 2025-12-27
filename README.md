# Project `led_test`
Getting started with STM32 development with a LED blink project

**Using these versions:**
* `STM32CubeIDE` : `1.18.1`
* `STM32CubeMX` : `6.14.1`

**Task 1: STM32 Setup & Basic Hardware Interface**

* **Get familiar with STM32CubeIDE:** Set up `STM32CubeMX`/`STM32CubeIDE`
  * Open `STM32CubeIDE`,  select **File -> New -> STM32 Project**
    * In the "STM32 Project" dialog, select the required board `NUCLEO-F411RE` and click "Next"
    * Set the "Project Name" and click "Finish"
    * **Don't initialise all peripherals!**
    * In the new `STM32CubeMX` tab, under the "Pinout & Configuration" top-tab...
      * click "Pinout" and then "Clear Pinouts"
      * Select `RCC`, set "High Speed Clock" to "Crystal/Ceramic Resonator"
      * Select `SYS`, set "Debug" to "Serial Wire"
    * In the new `STM32CubeMX` tab, under the "Clock Configuration" top-tab...
      * Select `HSE` on the "PLL Source Mux"
      * Set the `HCLK (MHz)` to 100 MHz and hity "Enter"
      * Save the tab changes. This should open the source code files
* **LED Setup:** Starting with basic GPIO to control, since there's only a single user LED on the `NUCLEO-F411RE`
  * Use STM32CubeMX to configure the GPIO pin for output mode
    * Check the "User Guide" to find out which pin is associated with the green user LED (`PA5`)
    * Click on **PA5** in the `led_test.ioc` file and select `GPIO_Output`
    * Right-click on **PA5** and type a User Label of `LED_GREEN`
  * Write a simple program to blink the LED
    * Add a private variable into the top of `main.c`:
      ```
      uint32_t delay_ms = 500;
      ```
    * Add the following into the `while` loop:
      ```
      	  HAL_GPIO_WritePin(LED_GREEN_GPIO_Port, LED_GREEN_Pin, GPIO_PIN_SET);
      	  HAL_Delay(delay_ms);

      	  HAL_GPIO_WritePin(LED_GREEN_GPIO_Port, LED_GREEN_Pin, GPIO_PIN_RESET);
      	  HAL_Delay(delay_ms);
      ```
      * *Notice the blocking code?*
    * Remember to build with `Ctrl+b` ;)
* **Learn a bit of STM32 HAL (Hardware Abstraction Layer):** This is the standard way to interface with peripherals like GPIOs, UART, SPI, etc., on STM32
