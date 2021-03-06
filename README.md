# LPC824 ADC DMA example

An example of how to use LPC824 to read data from the
ADC data registers directly to SRAM using Direct Memory Access (DMA). This allows
capturing data at the max data rate (1.2Msps) without any CPU intervention.

DMA transfers are limited to 1024 words. However
transfers can be chained to facilitate longer data capture. This is illustrated in
this example by chaining 3 DMA transfers of 1024 words/samples back-to-back. ADC
samples are triggered using the State Configurable Timer (SCT) to achieve regularing sampling intervals.

The ADC is configured to sample from one ADC channel (ADC3) and use SCT0_OUT3 as the trigger
for the sampling. The DMA is configured to transfer 16 bits from the ADC data register to 
SRAM. Since bits 15:4 of the ADC data register hold
the ADC value, a shift right of 4 bits (>>4) needs to be performed on each
sample by the CPU after capture to yield ADC values in range 0 - 4095.

This example is built upon examples provided by NXP for the LPC824. I recommend having
chapters 21 (ADC), 11,12 (DMA), 16 (SCT) of UM10800 LPC82x User Manual for reference.

## How to build

This project was created with LPCXpresso IDE (version 7.7.2). And has a dependency on the
LPCOpen Software Development Platform (LPC8xx packages) [1]

However it should also be 
possible to build without LPCXPresso using the GCC ARM Embedded compiler and the makefile 
in Debug directory. However right now that's not working. I need to figure some way
of packaging these LPCXpresso projects in a way that they can be compiled without
any dependencies other than GCC for ARM embedded. Any suggestions, please email
me (address below).

## Sample data 

The following is a ADC capture from a 40kHz ultrasound transducer at 500ksps. Just prior to the capture I taped the transducer to induce vibration.

![Scope screen grab](/data/ADC_DMA_scope_trace.png)

Joe Desbonnet
jdesbonnet@gmail.com
16 July 2015.

## References

[1] LPCOpen Software Development Platform (LPC8xx packages)
https://www.lpcware.com/content/nxpfile/lpcopen-software-development-platform-lpc8xx-packages

