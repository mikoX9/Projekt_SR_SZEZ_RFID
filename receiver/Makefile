

#	CC=xyz	->definiowanie zmiennej
#	$(CC)	->uzywanie zmiennej

MCU = atmega328p
MCU_ = m328p
F_CPU = 8000000


FILE1 		= lcdpcf8574
LOCATION1 	= lcdpcf8574

FILE2 		= pcf8574
LOCATION2 	= lcdpcf8574/pcf8574

FILE3 		= twimaster
LOCATION3 	= lcdpcf8574/i2chw

FILE4 		= rfm70
LOCATION4 	= rfm70


all:	main.hex
	rm -f main.o
	rm -f main.elf
	rm -f $(FILE1).o
	rm -f $(FILE2).o
	rm -f $(FILE3).o
	rm -f $(FILE4).o		
	avrdude -p $(MCU_) -c usbasp -e -U flash:w:main.hex

.c.o:
	avr-gcc -Wall -Os -DF_CPU=$(F_CPU) -c -mmcu=$(MCU) $(LOCATION1)/$(FILE1).c -o $(FILE1).o
	avr-gcc -Wall -Os -DF_CPU=$(F_CPU) -c -mmcu=$(MCU) $(LOCATION2)/$(FILE2).c -o $(FILE2).o
	avr-gcc -Wall -Os -DF_CPU=$(F_CPU) -c -mmcu=$(MCU) $(LOCATION3)/$(FILE3).c -o $(FILE3).o
	avr-gcc -Wall -Os -DF_CPU=$(F_CPU) -c -mmcu=$(MCU) $(LOCATION4)/$(FILE4).c -o $(FILE4).o
	avr-gcc -Wall -Os -DF_CPU=$(F_CPU) -c -mmcu=$(MCU) main.c -o main.o

main.elf: main.o $(FILE1).o $(FILE2).o $(FILE3).o $(FILE4).o
	avr-gcc -Wall -Os -DF_CPU=$(F_CPU) -mmcu=$(MCU) main.o $(FILE1).o $(FILE2).o $(FILE3).o $(FILE4).o -o main.elf

main.hex: main.elf
	rm -f main.hex
	avr-objcopy -j .text -j .data -O ihex main.elf main.hex

clean:
	rm -f main.hex
	rm -f main.o
	rm -f main.elf
	rm -f $(FILE1).o
	rm -f $(FILE2).o
	rm -f $(FILE3).o
	rm -f $(FILE4).o





###################################################################