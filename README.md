# Design of 1024*32 (4kB) SRAM 1.8V with access time &lt; 2.5ns using OpenRAM

This project aims to develop a 1024 *32 (4kB) SRAM with supply voltage 1.8V and access time < 2.5ns. Circuits required as inputs to the OpenRAM compiler are designed and simulated.

## Custom Cells Required for OpenRAM 
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

```
$ ngspice cell6T.cir
```

![](https://github.com/yash-k99/sram/blob/master/Waveforms/cell_read.PNG)

**-> Write Operation**

Open the cell6T.cir file. Comment the Read Operation commands and uncomment the write operation commands. Then run the following command:  
```
$ ngspice cell6T.cir
```

![](https://github.com/yash-k99/sram/blob/master/Waveforms/cell_write.PNG)

#### Analysis of 6T cell

##### **-> SNM Calculation**  
To obtain the SNM graphically, a butterfly curve is first plotted. For the measurement of the butterfly curve, the feedback of the cross-coupled inverter is separated. Then, DC analysis is performed at node q and node qb. Butterfly curve is obtained by toggling the 𝑋 and 𝑌 axis of one of the VTC curves, and merging the two separate VTC plots together. Shown below are the simulated butterfly curves of SRAM in hold mode, read mode and write operation. 

**1. Hold SNM**

```
$ ngspice holdsnm.cir
```

![](https://github.com/yash-k99/sram/blob/master/Waveforms/holdsnm.PNG)  
Fit the largest square in the two loops and find the hold SNM.

**2. Read SNM**

```
$ ngspice readsnm.cir
```

![](https://github.com/yash-k99/sram/blob/master/Waveforms/readsnm.PNG)  
Fit the largest square in the two loops and find the hold SNM.

**3. Write SNM**

```
$ ngspice writesnm.cir
```

![](https://github.com/yash-k99/sram/blob/master/Waveforms/writesnm.PNG)  
Fit the largest square and find the WNM.

##### **-> N-Curve**  

```
$ ngspice ncurve.cir
```

![](https://github.com/yash-k99/sram/blob/master/Waveforms/ncurve.PNG)
Stability Metrics:    
Static Voltage Noise Margin (SVNM) -> Difference between Pt C and Pt A  
Static Current Noise Margin (SINM) -> Pt B  
Write Trip Voltage (WTV) -> Difference between Pt E and Pt C  
Write Trip Current (WTI) -> Pt D  

### 2. Sense Amplifier

Run the netlist file using the following command:

``` 
$ ngspice senseamp.cir
```

![](https://github.com/yash-k99/sram/blob/master/Waveforms/senseamp.PNG)

### 3. Write Driver

Run the netlist file using the following command:

```
$ ngspice writedriver.cir
```

![](https://github.com/yash-k99/sram/blob/master/Waveforms/writedriver.PNG)

### 4. Tristate Buffer

Run the netlist file using the following command:

```
$ ngspice tristatebuff.cir
```

![](https://github.com/yash-k99/sram/blob/master/Waveforms/tristate.PNG)

### 5. Positive Edge Triggered DFF

Run the netlist file using the following command:

```
$ ngspice dff.cir
```

![](https://github.com/yash-k99/sram/blob/master/Waveforms/dff.PNG)

### 1-Bit SRAM  
![](https://github.com/yash-k99/sram/blob/master/Diagrams/1bitsram.PNG)

**-> Read Operation**

```
$ ngspice 1bitsram.cir
```

![](https://github.com/yash-k99/sram/blob/master/Waveforms/1bit_read.PNG)

**-> Write Operation**  
Open the 1bitsram.cir file. Comment out the read operation commands and uncomment the write operation command  
```
$ ngspice 1bitsram.cir
```

![](https://github.com/yash-k99/sram/blob/master/Waveforms/1bit_write.PNG)

# Author
Yash Kumar

# Acknowledgements  
* Kunal Ghosh, Director, VSD Corp. Pvt. Ltd.
* Philipp Gühring, Software Architect, LibreSilicon Assocation

# Contact Information  
* Yash Kumar, Undergraduate Student, Mumbai University - laryash99@gmail.com
* Kunal Ghosh, Director, VSD Corp. Pvt. Ltd. - kunalghosh@gmail.com
* Philipp Gühring, Software Architect, LibreSilicon Assocation - pg@futureware.at
