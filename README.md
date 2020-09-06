# Design of 1024*32 (4kB) SRAM 1.8V with access time &lt; 2.5ns using OpenRAM

This project aims to develop a 1024 *32 (4kB) SRAM with supply voltage 1.8V and access time < 2.5ns. Circuits required as inputs to the OpenRAM compiler are designed and simulated.

# Table of Contents  
- [Custom Cells Required for OpenRAM](#custom-cells-required-for-openram)  
- [Prelayout Simulations](#prelayout-simulations)  
- [Postlayout Simulations](#postlayout-simulations)  
- [Future Work](#future-work)  
- [Acknowledgements](#acknowledgements)  
- [Contact Information](#contact-information)  

# Custom Cells Required for OpenRAM 

![](https://github.com/yash-k99/vsdsram/blob/master/Diagrams/OpenRam.png)

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

### 6T Cell Stability

#### **-> SNM Calculation**  
The stability and writability of the cell are quantified by the hold margin, read margin and write margin which are determined by the static noise margin (SNM). It determines how much noise can be applied at the inputs of the two cross coupled inverters before a stable state is lost during hold or read operaring mode or a second stable state is created during write operation. 

**1. Hold SNM**

![](https://github.com/yash-k99/sram/blob/master/Diagrams/holdsnm.PNG)

```
$ ngspice holdsnm.cir
```

![](https://github.com/yash-k99/sram/blob/master/Waveforms/Prelayout/holdsnm.PNG)  
By fitting a square in the upper and lower loop, we get SNMh = 0.91V and SNMl = 0.61V respectively.  
Hold SNM = min (SNMh, SNMl) = 0.61V

**2. Read SNM**

![](https://github.com/yash-k99/sram/blob/master/Diagrams/readsnm.png)

```
$ ngspice readsnm.cir
```

![](https://github.com/yash-k99/sram/blob/master/Waveforms/Prelayout/readsnm.PNG)  
Similarly,  
Read SNM = min (SNMh, SNMl) = min (0.48V, 0.39V) = 0.39V

**3. Write SNM**

![](https://github.com/yash-k99/sram/blob/master/Diagrams/writesnm.PNG)

```
$ ngspice writesnm.cir
```

![](https://github.com/yash-k99/sram/blob/master/Waveforms/Prelayout/writesnm.PNG)  
By fitting the smallest square between the two curves, we get  
Write SNM = 1.065V

#### **-> N-Curve**  

N-curve provides the current flow information along with the voltage metrics which is equally important for an overall analysis of cell stability.    

![](https://github.com/yash-k99/sram/blob/master/Diagrams/ncurve.png)

```
$ ngspice ncurve.cir
```

![](https://github.com/yash-k99/sram/blob/master/Waveforms/Prelayout/ncurve.PNG)
**Read Stability Metrics**    

**Static Voltage Noise Margin (SVNM)** - It is the maximum tolerable dc noise voltage at internal nodes of the bitcell before its content flips and it is measured as the difference between point C and point A.  
SVNM = 0.617V

**Static Current Noise Margin (SINM)** - It is the maximum tolerable dc noise current injected at internal nodes of the bitcell before its content changes and it is denoted by point B.  
SINM = 255.67uA

**Write Stability Metrics**

**Write Trip Voltage (WTV)** - It is the minimum voltage drop needed to change the internal nodes of the bitcell and it is measured as the difference between point E and point C.  
WTV = 0.988V

**Write Trip Current (WTI)** - It is the minimum amount of current needed to write the bitcell and it denoted by point D.  
WTI = -53.47uA

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

![](https://github.com/yash-k99/vsdsram/blob/master/Layouts/cell6T.PNG)

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

![](https://github.com/yash-k99/vsdsram/blob/master/Layouts/senseamp.PNG)

Run the netlist file using the following command:

``` 
$ ngspice senseamp.spice
```

![](https://github.com/yash-k99/sram/blob/master/Waveforms/Postlayout/senseamp.PNG)

### 3. Write Driver

![](https://github.com/yash-k99/vsdsram/blob/master/Layouts/writedriver.PNG)

Run the netlist file using the following command:

```
$ ngspice writedriver.spice
```

![](https://github.com/yash-k99/sram/blob/master/Waveforms/Postlayout/writedriver.PNG)

### 4. Tristate Buffer

![](https://github.com/yash-k99/vsdsram/blob/master/Layouts/tristate.PNG)

Run the netlist file using the following command:

```
$ ngspice tri.spice
```

![](https://github.com/yash-k99/sram/blob/master/Waveforms/Postlayout/tristate.PNG)

### 5. Positive Edge Triggered DFF

![](https://github.com/yash-k99/vsdsram/blob/master/Layouts/dff.PNG)

Run the netlist file using the following command:

```
$ ngspice dff.spice
```

![](https://github.com/yash-k99/sram/blob/master/Waveforms/Postlayout/dff.PNG)

### 1-Bit SRAM  

![](https://github.com/yash-k99/vsdsram/blob/master/Layouts/1bitsram.PNG)

**-> Read Operation**

```
$ ngspice 1bitsram_read.spice
```

![](https://github.com/yash-k99/sram/blob/master/Waveforms/Postlayout/1bit_read.PNG)

**-> Write Operation**  
  
```
$ ngspice 1bitsram_write.spice
```

![](https://github.com/yash-k99/sram/blob/master/Waveforms/Postlayout/1bit_write.PNG)


# Future Work

* Porting OSU018 technology to OpenRAM and adding the above created custom cells to it. 

# Acknowledgements  
* Kunal Ghosh, Co-founder, VSD Corp. Pvt. Ltd.
* Philipp Gühring, Software Architect, LibreSilicon Assocation

# Contact Information  
* Yash Kumar, B.E. Electronics, Fr. Conceicao Rodrigues College of Engineering, Mumbai - laryash99@gmail.com
* Kunal Ghosh, Director, VSD Corp. Pvt. Ltd. - kunalghosh@gmail.com
* Philipp Gühring, Software Architect, LibreSilicon Assocation - pg@futureware.at
