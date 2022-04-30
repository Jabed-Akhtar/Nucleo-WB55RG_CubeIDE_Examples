# Nucleo-WB55RG_CubeIDE

> main file is saved at location '\<project-name>\Core\Src\main.c'

## User LEDs
LED1 -> PB5, Blue  
LED2 -> PB0, Green  
LED3 -> PB1, Red  

## Simple BLE Config
1. Enable RCC (System Core)  
	: HSE -> Crystal/Ceramic Resonator  
	: LSE -> Crystal/Ceramic Resonator  
2. Activate HSEM (System Core)  
	|- NVIC Settings  
		: HSEM global interrupt -> Enabled  
3. Activate IPCC (System Core)  
	|- NVIC Settings  
		: IPCC RX occupied interrupt -> Enabled  
		: IPCC TX free interrupt -> Enabled  
4. Activate RTC (Timers)  
	: WakeUp -> Internal WakeUp  
	|- NVIC Settings  
		: RTC wake-up interrupt through EXTI line 19 -> Enabled  
5. Activate RF (Connectivity)  
6. Enable and configure USART1 (Connectivity)  
	: Mode -> Asynchronous  
	|- Parameter Settings  
		: Baudrate -> 115200 Bits/s  
		: Word Length -> 8 Bits (including Parity)  
		: Parity -> None  
		: Stop Bits -> 1  
	|- DMA Settings  
		: Add -> USART1_RX  
		: Add -> USART1_TX  
	|- NVIC Settings  
		: DMA1 channel1 global interrupt -> Enabled  
		: DMA1 channel2 global interrupt -> Enabled  
		: USART1 global interrupt -> Enabled  
7. Enable and configure BLE (Middleware)  
	|- BLE Applications and Services  
		: Custon P2P Server -> Disabled  
		: Custom Template -> Enabled  
	|- Configurations  
		: HW UART > CFG_HW_USART1_ENABLED -> Enabled (at this step, 8. is very important)  
		: HW UART > CFG_HW_USART1_DMA_TX_SUPPORTED -> Enabled  
		: Application parameters > CFG_DEBUG_TRACE_UART -> hw_uart1  
		: Generic parameters > CFG_DEBUG_APP_TRACE -> Enabled  
	|- BLE Advertising  
		: Advertising elements > Include AD_TYPE_COMPLETE_LOCAL_NAME element -> Yes  
			: AD_TYPE_COMPLETE_LOCAL_NAME -> <Name> (e.g. STM32-BLE)  
	|- BLE GATT  
		: Services configuration > Number of services -> 1  
		: Service1 > Service long name -> <Name> (e.g. MY_SRV)  
		: Service1 > Service short name -> <Name> (e.g. MY_SRV)  
	|- <Service Name>  
		: Service1 > Number of characteristics -> 1  
		: Characteristics1 general > Characteristics long name -> <Name> (e.g. MY_CHAR)  
		: Characteristics1 general > Characteristics short name -> <Name> (e.g. MY_CHAR)  
		: Characteristics1 properties > CHAR_PROP_BROADCAST -> No  
		: Characteristics1 properties > CHAR_PROP_READ -> Yes  
		: Characteristics1 GATT events > GATT_NOTIFY_ATTRIBUTE_WRITE -> No  
		: Characteristics1 GATT events > GATT_NOTIFY_WRITE_REQ_AND_WAIT_FOR_APPL_RESP -> No  
		: Characteristics1 GATT events > GATT_NOTIFY_READ_REQ_AND_WAIT_FOR_APPL_RESP -> No  
8. Go to 'Project Manager' > 'Advanced Settings'  
	-> MX_USART1_UART_Init -> 'Do not Generate Function Call' -> ticked and 'Visibility (Static)' -> unticked  
9. Clock Configuration  
		: HCLK1 (MHz) -> 32  
		: HCLK2 (MHz) -> 32  
		: RTC/LCD Source Mux -> LSE  
		: RFWKP Clock Mux -> LSE  
