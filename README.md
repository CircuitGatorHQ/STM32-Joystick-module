# STM32-Joystick-module
This is a simple code for using an analog Joystick module with an STM32 Microcontroller, the full tutorial video is available on YouTube: https://youtu.be/rQGIqen2qxA


    /* Private includes ----------------------------------------------------------*/
    /* USER CODE BEGIN Includes */
    #include <stdio.h>
    #include "string.h"
    /* USER CODE END Includes */
    
    /* USER CODE BEGIN PV */
    uint16_t xValue;
    uint16_t yValue;
    uint32_t readValue[2];
    uint8_t button_state;
    char buffer[50];
    /* USER CODE END PV */
    
    
    /* USER CODE BEGIN 2 */
    HAL_ADC_Start_DMA(&hadc1, (uint32_t*)readValue, 2);
    /* USER CODE END 2 */
    
    /* USER CODE BEGIN 3 */
    for (uint8_t i =0; i<hadc1.Init.NbrOfConversion; i++){
      xValue = (uint16_t) readValue[0];
      yValue = (uint16_t) readValue[1];
    }
    button_state = HAL_GPIO_ReadPin(GPIOA, GPIO_PIN_8);
    snprintf(buffer, sizeof(buffer), "xValue: %d,yValue: %d, button: %d\r\n", xValue,yValue,button_state);
    HAL_UART_Transmit(&huart2, (uint8_t*)buffer, sizeof(buffer), HAL_MAX_DELAY);
    HAL_Delay(500);
    /* USER CODE END 3 */
