## 3 to 8 decoder
![[Pasted image 20231103090634.png]]
This decoder is used when you have several memory chipsets that are used to form an address block.
• The Y-outputs are fed to the CS on the circuits
• The address pins that do not fit on the memory chipsets (A15-17) are placed on A, B and C on the 74xx137, which are used to select a specific chipset
• If there are multiple address pins left (A18-19), they are used to select the 74xx137 via the CS pin

## 2 to 4 decoder
![[Pasted image 20231103091202.png]]

## Programmable Array Logic
This type of address demultiplexer circuit can be programmed with Boolean algebra
![[Pasted image 20231103091249.png]]