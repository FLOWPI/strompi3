# Open-Source Firmware for the Joy-IT StromPi 3
******************************************************************************************************************

StromPi v3 - by Joy-IT
OpenSource-Firmware published under MIT-License

******************************************************************************************************************

This following pieces of Code defines the Firmware of the StromPi3 Raspberry Pi expansion.
	Its main functions are included into the integrated OpenSource FreeRTOS
	The Basis I/O HAL Drivers of the STM32F031 are generated with STM32CubeMX and can be modified here in Source
	or with the "StromPi3.ioc" - File.

	The main functionality of the StromPi3 is realized with the STM32 ADC Watchdog - which is configured to monitor
	the voltage of the configured primary voltage source. If the voltage source fails and the measured voltage
	falls under the threshold, then the STM32 switch to the voltage/powerpath of the configured backup source.
	The STM32 switches the powerpath through Mosfets connected to its GPIO-Ports.
	The voltage-sources which can be configured are the following:

		- mUSB
		- Wide-Range (StepDown Regulator Output)
		- Battery

	If the Battery-PowerPath isn't selected as the voltage-source, the Battery-Hat Expansion would be configured
	into its charging mode.
	For further reference of the topology of the StromPi3, please refer to the schematic-files which are also
	included into the OpenSource-Files

	The FreeRTOS Operating System is generated with two Tasks:

		- Main Operating Task with the AlarmHandler (for Time based Operations like timed WakeUp or Shutdown),
		  the function to repower the Raspberry Pi in case that the main voltage source comes back
		  and the functions to read out the ADC-Values for Voltage Output.
		  This Task is timed to operate in a period of 1 second

		  The Sourcecode of this Task is defined in this "main.c" File

		- Serial Console Task which is processing the the in- and output of the serial interface.

		  The Sourecode of this Task is defined in the "UART_CLI.c" File

 	The ADC-Watchdog is processed in its own HAL-Based Interrupt-Routine through flags, which then are
 	processed in the main Task.
	
	Further Informations about the Schematic and the PCB Layout of the StromPi3, 
	you can find in the "Schematic+Hardware-Layout"-Folder.

 	The Files are created in the Atollic TrueSTUDIO for STM32, which can be used for STM32 for free.
 	You can include the .cproject file in the IDE and start to code your own modifications
 	and debug them with a ST-Linkv2 connected to the StromPi3 or make your own binary which can be flashed
 	with the stm32flasher in flashmode of the StromPi 3
 	(Please refer to the manual provided in our firmware updates in the download section of strompi.joy-it.net)

 	(connections have to be soldered for InCircuit debugging- please refer to the Hardware-Layout provided in 
	the "Schematic Files+Hardware-Layout" Folder)

 	Please refer to the additional comments in the corresponding sections for further explanations.

	If there are questions or something is unclear, please feel free
	to contact us via E-Mail: service@joy-it.net
	