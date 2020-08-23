# Design of 1024*32 (4kB) SRAM 1.8V with access time &lt; 2.5ns using OpenRAM

This project aims to develop a 1024 *32 (4kB) SRAM with supply voltage 1.8V and access time < 2.5ns. Circuits required as inputs to the OpenRAM compiler are designed and simulated.

## Custom Cells Required for OpenRAM 
* SRAM Bit cell  
* Sense Amplifier  
* Write Driver  
* Tristate Buffer  
* D-Flip Flop  

# Prelayout Simulations  
To clone the Repository and download the Netlist files for Simulation, enter the following commands in your terminal.  
```
$  sudo apt install -y git
$  git clone https://github.com/yash-k33/vsdsram
$  cd vsdsram/Simulation/Prelayout
```

### 1. 6T Cell

![](https://github.com/yash-k99/sram/blob/master/Diagrams/6Tcell.png)

**-> Read Operation**  

```
$ ngspice cell6T_read.cir
```

![](https://github.com/yash-k99/vsdsram/blob/master/Waveforms/Prelayout/cell_read.PNG)

**-> Write Operation**
  
```
$ ngspice cell6T_write.cir
```

![](https://github.com/yash-k99/vsdsram/blob/master/Waveforms/Prelayout/cell_write.PNG)

#### Analysis of 6T cell

##### **-> SNM Calculation**  
To obtain the SNM graphically, a butterfly curve is first plotted. For the measurement of the butterfly curve, the feedback of the cross-coupled inverter is separated. Then, DC analysis is performed at node q and node qb. Butterfly curve is obtained by toggling the 𝑋 and 𝑌 axis of one of the VTC curves, and merging the two separate VTC plots together. Shown below are the simulated butterfly curves of SRAM in hold mode, read mode and write operation. 

**1. Hold SNM**

![](https://github.com/yash-k99/sram/blob/master/Diagrams/holdsnm.PNG)

```
$ ngspice holdsnm.cir
```

![](https://github.com/yash-k99/sram/blob/master/Waveforms/Prelayout/holdsnm.PNG)  
Fit the largest square in the two loops and find the hold SNM.

**2. Read SNM**

![](https://github.com/yash-k99/sram/blob/master/Diagrams/readsnm.png)

```
$ ngspice readsnm.cir
```

![](https://github.com/yash-k99/sram/blob/master/Waveforms/Prelayout/readsnm.PNG)  
Fit the largest square in the two loops and find the hold SNM.

**3. Write SNM**

![](https://github.com/yash-k99/sram/blob/master/Diagrams/writesnm.PNG)

```
$ ngspice writesnm.cir
```

![](https://github.com/yash-k99/sram/blob/master/Waveforms/Prelayout/writesnm.PNG)  
Fit the largest square and find the WNM.

##### **-> N-Curve**  

![](https://github.com/yash-k99/sram/blob/master/Diagrams/ncurve.png)

```
$ ngspice ncurve.cir
```

![](https://github.com/yash-k99/sram/blob/master/Waveforms/Prelayout/ncurve.PNG)
Stability Metrics:    
Static Voltage Noise Margin (SVNM) -> Difference between Pt C and Pt A  
Static Current Noise Margin (SINM) -> Pt B  
Write Trip Voltage (WTV) -> Difference between Pt E and Pt C  
Write Trip Current (WTI) -> Pt D  

### 2. Sense Amplifier

![](https://github.com/yash-k99/sram/blob/master/Diagrams/senseamp.png)

Run the netlist file using the following command:

``` 
$ ngspice senseamp.cir
```

![](https://github.com/yash-k99/sram/blob/master/Waveforms/Prelayout/senseamp.PNG)

### 3. Write Driver

![](https://github.com/yash-k99/sram/blob/master/Diagrams/writedriver.PNG)

Run the netlist file using the following command:

```
$ ngspice writedriver.cir
```

![](https://github.com/yash-k99/sram/blob/master/Waveforms/Prelayout/writedriver.PNG)

### 4. Tristate Buffer

![](https://github.com/yash-k99/sram/blob/master/Diagrams/tristate.png)

Run the netlist file using the following command:

```
$ ngspice tristatebuff.cir
```

![](https://github.com/yash-k99/sram/blob/master/Waveforms/Prelayout/tristate.PNG)

### 5. Positive Edge Triggered DFF

![](https://github.com/yash-k99/sram/blob/master/Diagrams/dff.png)

Run the netlist file using the following command:

```
$ ngspice dff.cir
```

![](https://github.com/yash-k99/sram/blob/master/Waveforms/Prelayout/dff.PNG)

### 1-Bit SRAM  
![](https://github.com/yash-k99/sram/blob/master/Diagrams/1bitsram.PNG)

**-> Read Operation**

```
$ ngspice 1bitsram_read.cir
```

![](https://github.com/yash-k99/sram/blob/master/Waveforms/Prelayout/1bit_read.PNG)

**-> Write Operation**  
  
```
$ ngspice 1bitsram_write.cir
```

![](https://github.com/yash-k99/sram/blob/master/Waveforms/Prelayout/1bit_write.PNG)

# Postlayout Simulations

  
```
$  cd vsdsram/Simulation/Postlayout
```

### 1. 6T Cell

**-> Read Operation**  

```
$ ngspice cell6T_read.spice
```

![](https://github.com/yash-k99/vsdsram/blob/master/Waveforms/Postlayout/cell_read.PNG)

**-> Write Operation**
  
```
$ ngspice cell6T_write.spice
```

![](https://github.com/yash-k99/vsdsram/blob/master/Waveforms/Postlayout/cell_write.PNG)

### 2. Sense Amplifier

Run the netlist file using the following command:

``` 
$ ngspice senseamp.spice
```

![](https://github.com/yash-k99/sram/blob/master/Waveforms/Postlayout/senseamp.PNG)

### 3. Write Driver

Run the netlist file using the following command:

```
$ ngspice writedriver.spice
```

![](https://github.com/yash-k99/sram/blob/master/Waveforms/Postlayout/writedriver.PNG)

### 4. Tristate Buffer

Run the netlist file using the following command:

```
$ ngspice tri.spice
```

![](https://github.com/yash-k99/sram/blob/master/Waveforms/Postlayout/tristate.PNG)

# Author
Yash Kumar

# Acknowledgements  
* Kunal Ghosh, Director, VSD Corp. Pvt. Ltd.
* Philipp Gühring, Software Architect, LibreSilicon Assocation

# Contact Information  
* Yash Kumar, Undergraduate Student, Mumbai University - laryash99@gmail.com
* Kunal Ghosh, Director, VSD Corp. Pvt. Ltd. - kunalghosh@gmail.com
* Philipp Gühring, Software Architect, LibreSilicon Assocation - pg@futureware.at
