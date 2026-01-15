$\text{I}^2\text{C}$ bus or Inter-Intergrated Circuit bus is a serial Multi-master/slave bus.
I2C was developed by Philips Semiconductors in 1982. Since 2006, I2C protocol has been license-free. However, you still have to pay a license for I²C slave addresses allocated by NXP. NXP is a Dutch semiconductor manufacturer I2C is primarily used for low-speed applications where a microcontroller (master) is required to connect to peripheral IC circuits (slaves).
I2C is used over short distances as intra-board communication in areas such as:
▪ Embedded systems
▪ Cell phones
▪ And so on…

I2C offers a connection-oriented protocol with acknowledge, and uses only 2 wires for this:
▪ SCL – Serial clock
▪ SDA – Serial data
![[Pasted image 20231205131525.png]]
Since I2C devices use only 2 bidirectional open-drain pins for data communication, there must be a pull-up resistor on each of bus lines. This simultaneously provides a wired-AND function, which is used in the I2C protocol.

Since I2C is a synchronous protocol, we of course have both Clock and Data.
The rule is:
▪ data is stable when Clock is high
▪ data may change when Clock is low
![[Pasted image 20231205131711.png]]
Each data bit transferred on the SDA line is synchronized by a high-to-low pulse of clock on the SCL line.
The only exception to this is the START and STOP conditions.

## Start and Stop conditions
As mentioned, the I2C protocol is connection-oriented. It means that:
▪ A transmission starts with a START condition
▪ A transmission ends with a STOP condition
▪ START and STOP conditions are controlled by the master
![[Pasted image 20231205131830.png]]
START condition: SDA switches from high to low while SCL is high
STOP condition: SDA switches from low to high while SCL is high
This makes START and STOP different from other communications
See previous page (data is stable when SCL is high)

### Repeated start condition
The bus is busy between START and STOP during each transmission.
If a master wants to maintain control of the bus over several
transmissions, then REPEATED START can be done.
Example:
If you want to read coherent data from a table without others being
able to correct the table before you have finished reading it all.
![[Pasted image 20231205132047.png]]

## Packet Format
Address and Data information that is to be transmitted via I2C bus must be packed in a frame.
▪ A frame is 9 bits long.
▪ The first 8 bits come from the transmitter
▪ The last bit is left to the receiver, here ACK or NACK is sent back to the transmitter.
![[Pasted image 20231205132141.png]]
A complete data transfer consists of:
START + Address packet + n Data packet(s) + STOP
### Address Packet format - 7 bit
There are 128 slave addresses on the same bus, but that does not mean that there can also be 128 slave devices.
![[Pasted image 20231205132352.png]]
Address 0000 000 is a broadcast address for all devices.
The top 8 addresses in the format of 1111xxx are reserved.
This means that there are 119 addresses left for slave devices.
The eighth bit in the packet is the READ/WRITE control bit. If this bit is set, the master will read the next frame from the slave, otherwise, the master will write the next frame on the bus to the slave. This is different from SPI, where the control bit is the first bit.
In the I2C bus, the MSB of the address is transmitted first.
#### Example:
A Master sends data to a Slave with address 1001101
1) The master puts a high-to-low pulse on SDA, while SCL is high to generate a start bit condition to start the transmission.
2) The master transmits 10011010 into the bus. The first seven bits (1001101) indicates the slave address, and the eighth bit (0) indicates a Write operation and says that the master will write the next byte (data) into the slave.
![[Pasted image 20231205132717.png]]
### Address Packet format - 10 bit
Although it is not mentioned in the book, there is also a completely legal 10-bit address format in the protocol.
This gives 1023 slave devices + a Broadcast address
![[Pasted image 20231205132843.png]]

### Data Packet format
▪ Just like Address packets, data packets also consist of 9 bits
▪ Just like in Address packets, MSB is sent first
![[Pasted image 20231205133137.png]]
If the receiver has received the last byte of data or it can not receive or process more, then a NACK is sent by leaving the SDA line high. This tells the sender that the transmission is over or that more bits can only be sent later.
#### Example:
![[Pasted image 20231205133224.png]]

## Flow control
One of the features of the I2C protocol is the ability to hold the clock line
(SCL). This is called Clock Stretching as a kind of flow control.
![[Pasted image 20231205133354.png]]
If a slow addressed slave device is not ready to process more data, it is able to stretch the clock by holding the SCL line.
The master will not be able to raise the clock line (because devices are wire-ANDed) and will wait until the slave releases the SCL line to show it is ready to transfer the next bit.

## Arbitration - bus access mechanism
▪ The I2C protocol supports multi-master configuration.
▪ There may be several master nodes in the system, but only one master can be active at a time.
![[Pasted image 20231205133500.png]]
When two or more masters initiate a transmission at about the same time, in this case, the Arbitration happens.

### Example:
![[Pasted image 20231205133602.png]]

## Multibyte burst write
I2C supports burst write. This method is especially effective if writing to a slave's memory block.
![[Pasted image 20231205133746.png]]
▪ First write the address of the slave node (here the last bit shows a WR)
▪ Then write the first location of the memory block in the slave node.
▪ Finally, data is sent into the selected memory block of the selected slave.

## Multibyte Burst read
Of course, the I2C also supports burst read. This method is effective for the same reasons as burst write.
![[Pasted image 20231205133913.png]]
▪ First write the address of the slave node (here the last bit shows a WR)
▪ Then write the first location on the memory block in the slave.
▪ Now a REPEATED START is sent to hold on to the bus
▪ Then the slave node's address is written again (here the last bit shows a RD)
▪ Finally, data from the selected memory block of the selected slave is read

# I2C Registers
## Two Wire Interface - TWI
![[Pasted image 20231205134122.png]]

## TWI Bit Rate Register (TWBR)
This register contains the division factor which, together with the
Prescaler bit (TWPS \[1: 0]) in the status register, controls the SCL.

## TWI Status Register (TWSR)
TWS\[7:3]: TWI Status
▪ These 5 bits show the status (as codes) of the TWI logic and TWI bus.
TWPS\[1:0]: TWI Prescaler Bits
▪ These 2 bits together with the TWBR register control the
speed of the bus (SCL frequency).

## TWI Control Register (TWCR)
TWINT: TWI Interrupt
▪ This flag is set when a data transfer is over.
▪ If TWI and general Interrupt are enabled, then an interrupt is
initiated when this flag is set to one.
▪ This flag must be cleared by software.

TWEA: TWI Enable Acknowledge
▪ Once this bit is set, ACK is generated when needed in slave or
receiver mode.

TWSTA: TWI START condition Bit
▪ When this bit is set, a START condition is generated if the
bus is free.
▪ If the bus is not available, then wait until it becomes
free. Then a START condition is generated.

TWSTO: TWI STOP condition Bit
▪ If one is in the master mode, then a STOP condition will
be initiated when this bit is set.
▪ The bit is cleared when STOP condition is performed.

TWWC: TWI Write Collision Flag
▪ This flag is set if you try to access the TWI Data Register when
the TWINT flag is not set.
▪ This flag is deleted when writing to the TWI Data Register
while the TWINT flag is set.

TWEN: TWI Enable
When this flag is set, the TWI module is enabled

TWIE: TWI Interrupt Enable
▪ This flag must be set if you want to use interrupt control.
It requires writing an interrupt service routine

## TWI Data Register (TWDR)
▪ In receiver mode, this register will contain the last received byte.
▪ In sender mode, you must write the next byte you want to send to this register
Remember that you must only access this register when the TWINT
of TWCR register is set.

## TWI Address Register (TWAR)
▪ ATmega32 supports 7-bit addressing.
▪ This register contains the address to which the device will respond when working in the slave mode.

TWGCE: TWI General Call Recognition Enable
▪ If this bit is set, then it also responds to the broadcast address:
address 0000 000
▪ If this bit is set, receiving a broadcast address will cause an
interrupt request.
