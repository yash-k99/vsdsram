# Design of 1024*32 (4kB) SRAM 1.8V with access time &lt; 2.5ns using OpenRAM

This project aims to develop a 1024 *32 (4kB) SRAM with supply voltage 1.8V and access time < 2.5ns. Circuits required as inputs to the OpenRAM compiler are designed and simulated.

## Inputs required for OpenRAM 
* SRAM Bit cell  
* Sense Amplifier  
* Write Driver  
* Tristate Buffer  
* D-Flip Flop  

## Prelayout Simulations  
To clone the Repository and download the Netlist files for Simulation, enter the following commands in your terminal.  
```
$  sudo apt install -y git
$  git clone https://github.com/yash-k33/sram
$  cd sram/Simulation/Prelayout
```

### 1. 6T Cell
**-> Read Operation**  

`$ ngspice cell6T.cir`

![](https://github.com/yash-k99/sram/blob/master/Waveforms/cell_read.PNG)

**-> Write Operation**

Open the cell6T.cir file. Comment the Read Operation commands and uncomment the write operation commands. Then run the following command:  
`$ ngspice cell6T.cir`

![](https://github.com/yash-k99/sram/blob/master/Waveforms/cell_write.PNG)

#### Analysis of 6T cell

##### **-> SNM Calculation**
**1. Hold SNM**

`$ ngspice holdsnm.cir`

![](https://github.com/yash-k99/sram/blob/master/Waveforms/holdsnm.PNG)

Fit the largest square in the two loops and find the hold SNM.

**2. Read SNM**

`$ ngspice readsnm.cir`

![](https://github.com/yash-k99/sram/blob/master/Waveforms/readsnm.PNG)

Fit the largest square in the two loops and find the hold SNM.

**3. Write SNM**

`$ ngspice writesnm.cir`

![](https://github.com/yash-k99/sram/blob/master/Waveforms/writesnm.PNG)

##### **-> N-Curve**

`$ ngspice ncurve.cir`

![](https://github.com/yash-k99/sram/blob/master/Waveforms/ncurve.PNG)

### 2. Sense Amplifier

`$ ngspice senseamp.cir`

![](https://github.com/yash-k99/sram/blob/master/Waveforms/senseamp.PNG)

### 3. Write Driver

`$ ngspice writedriver.cir`

![](https://github.com/yash-k99/sram/blob/master/Waveforms/writedriver.PNG)

### 4. Tristate Buffer

`$ ngspice tristatebuff.cir`

![](https://github.com/yash-k99/sram/blob/master/Waveforms/tristate.PNG)

### 5. Positive Edge Triggered DFF

`$ ngspice dff.cir`

![](https://github.com/yash-k99/sram/blob/master/Waveforms/dff.PNG)

### 1-Bit SRAM  
**-> Read Operation**

`$ ngspice 1bitsram.cir`

![](https://github.com/yash-k99/sram/blob/master/Waveforms/1bit_read.PNG)

**-> Write Operation**  
Open the 1bitsram.cir file. Comment out the read operation commands and uncomment the write operation command  
`$ ngspice 1bitsram.cir`

![](https://github.com/yash-k99/sram/blob/master/Waveforms/1bit_write.PNG)
