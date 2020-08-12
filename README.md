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
The best measure to quantify the stability of an SRAM bitcell during the read cycle and in hold state is the Static Noise Margin (SNM). The SNM is defined as the maximum amount of DC noise (VN) that can be tolerated by the cross-coupled inverter pair such that the bitcell retains its data. The read SNM is extracted from the read voltage transfer characteristics (VTC). The read VTC can be measured by sweeping the voltage at the data storage node Q (or QB) with both bitlines (BL, BLB) and wordline (WL) biased at VDD while monitoring the node voltage at QB (or Q). The write-ability of a SRAM bitcell can be gauged by the write SNM. The write SNM is extracted by a combination of read voltage transfer characteristics (VTC) and the write VTC.  

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
Another attractive approach which N-curve contains information for both read stability and write stability. There is no need of mathematical manipulation on the measured data as N-curve directly provides the functional information of SRAM bitcell. N-curve contains information for both voltage and current. Thus, allowing a complete functional analysis of the SRAM bitcell stability for both read and write operations with only one N-curve.

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
