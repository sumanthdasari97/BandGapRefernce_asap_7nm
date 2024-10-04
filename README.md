# BandGapRefernce_asap_7nm
# Overview of ASAP-7nm
ASAP7nm is a process design kit (PDK) created by the collaboration between academia and the semiconductor industry, specifically the Academia and Semiconductor Industrial Partnership (ASIP) consortium. This PDK provides access to cutting-edge semiconductor fabrication technologies at the 7-nanometer (nm) technology node. It includes necessary files and documentation for designing integrated circuits (ICs) that boast higher transistor density, enhanced performance, and lower power consumption. Designed for researchers, educators, and industry professionals, ASAP7nm promotes experimentation, educational initiatives, and collaboration in the field of semiconductor engineering. This fosters innovative IC design, practical learning experiences, and prototyping ahead of commercial production.

To install this PDK, you can clone the repository available at https://github.com/The-OpenROAD-Project/asap7.git

To install this PDK, you can clone the repository available at
 
 Xschem Installation for Ubuntu 

Open Your Terminal in your ubuntu workstation and execute the following command one by one or copy them into a script and run the script using the terminal.
```bash
# Install xschem, a schematic capture tool
git clone https://github.com/StefanSchippers/xschem.git xschem
cd xschem
./configure
make
sudo make install
cd ..
```

Ngspice Installation for Ubuntu 
Open Your Terminal  your ubuntu workstation and execute the following command one by one or copy them into a script and run the script using the terminal.
```bash
## clone the source repository into a local ngspice_git directory
git clone https://git.code.sf.net/p/ngspice/ngspice ngspice_git
cd ngspice_git
mkdir release
./autogen.sh
cd release
../configure --with-x --enable-xspice --disable-debug --enable-cider --with-readline=yes --enable-openmp --enable-osdi
## build the program
make
## install the program and needed files.
sudo make install
```

Add 7nm model .sch file for FinFET characterization

- Integrated the 7nm model .sch file from an external GitHub repository.
```bash
git clone https://github.com/AsahiroKenpachi/asap_7nm_Xschem.git

  ```


N- Finfet Characterestics
The characterization of an N-channel FinFET (Field-Effect Transistor) at the 7nm technology node. N-FinFETs are advanced multi-gate transistors that provide better control over the channel, reduce leakage currents, and enhance device performance compared to traditional planar technologies.
```
v {xschem version=3.4.5 file_version=1.2
}
G {}
K {}
V {}
S {}
E {}
N 170 90 170 120 {
lab=GND}
N 170 60 240 60 {
lab=GND}
N 240 60 240 110 {
lab=GND}
N 170 110 240 110 {
lab=GND}
N 170 10 170 30 {
lab=nfet_out}
N 100 20 170 20 {
lab=nfet_out}
C {vsource.sym} -40 100 0 0 {name=V1 value=0 savecurrent=false}
C {gnd.sym} 170 120 0 0 {name=l1 lab=GND}
C {gnd.sym} -40 130 0 0 {name=l2 lab=GND}
C {lab_pin.sym} -40 70 0 0 {name=p1 sig_type=std_logic lab=nfet_in}
C {lab_pin.sym} 130 60 0 0 {name=p2 sig_type=std_logic lab=nfet_in}
C {vsource.sym} 370 100 0 0 {name=V2 value=3 savecurrent=false}
C {gnd.sym} 370 130 0 0 {name=l3 lab=GND}
C {lab_pin.sym} 370 70 0 0 {name=p3 sig_type=std_logic lab=vdd}
C {lab_pin.sym} 170 -50 0 0 {name=p4 sig_type=std_logic lab=vdd}
C {code_shown.sym} 430 20 0 0 {name=s1 only_toplevel=false value="
.dc v1 0 0.7 1m v2 0 0.7 0.2
.control
run
set xbrushwidth=3
let vd = vdd - nfet_out
let id  = vd/1000
plot id
.endc
"}
C {res.sym} 170 -20 0 0 {name=R1
value=1k
footprint=1206
device=resistor
m=1}
C {lab_pin.sym} 100 20 0 0 {name=p5 sig_type=std_logic lab=nfet_out}
C {/home/dasari/Desktop/asap_7nm_Xschem/asap_7nm_nfet.sym} 150 60 0 0 {name=nfet2 model=asap_7nm_nfet spiceprefix=X l=7e-009 nfin=14}
```
<p align="center">
  <img src="https://github.com/user-attachments/assets/c93f3269-87e2-4486-aa04-c84e4c9d098a" width="45%" />
  <img src="https://github.com/user-attachments/assets/a0abe8e1-db49-4b45-9dd3-5fb7ad152af1" width="45%" />
</p>

<p align="center">
  <b>Figure 1:</b> N-FinFET Characterization Graph for nfin = 14 &nbsp;&nbsp;&nbsp;&nbsp;
  <b>Figure 2:</b> N-FinFET Characterization Graph for nfin = 32
</p>

The current in the N-FinFET increases as the number of fins (nfin) increases. This behavior is evident in both Figure 1 and Figure 2, where higher values of nfin correspond to a noticeable increase in drain current (Id). This occurs because increasing the number of fins effectively increases the total width of the transistor, allowing for more current to flow through the device under the same bias conditions.



### Inverter VTC Characterization

Performing characterization of the voltage transfer characteristics (VTC) of an inverter with varying W/L ratios for PFET and NFET. The key parameters being measured include:

- **Threshold Voltage (Vth)**
- **Drain Current (Id)**
- **Gate Capacitance (Cg)**
- **Power Consumption (P)**
- **Propagation Delay (t_pd) (ps)**
- **Gain (Av)**
- **Input Low Voltage (vil)**
- **Output Low Voltage (vol)**
- **Noise Margin Low (nml)**
- **Output High Voltage (voh)**
- **Input High Voltage (vih)**
- **Noise Margin High (nmh)**
- **Transconductance (gm)**
- **Frequency (f)**
- **Output Resistance (Ro)**

This characterization allows me to analyze how different transistor sizing affects the inverter's performance in terms of switching behavior, speed, power efficiency, and noise margins.

| Sr. No | W (Width) PMOS | L (Length) PMOS | (W/L Ratio) PMOS | W (Width) NMOS | L (Length) NMOS | (W/L Ratio) NMOS | Threshold Voltage (Vth) | Drain Current (Id)  | Propagation Delay (t_pd) (ps) | Gain (Av) | vil     | vol  | NML     | voh  | vih     | NMH     |
|--------|-----------------|-----------------|------------------|----------------|-----------------|------------------|-------------------------|---------------------|-----------------------------|-----------|---------|------|---------|------|---------|---------|
| 1      | 14              | 7               | 2                | 14             | 7               | 2                | 0.3447862                | 0.000226364         | 0.0066385                   | 6.41489   | 0.2939  | 0    | 0.2939  | 0.7  | 0.428431| 0.271569 |
| 2      | 16              | 7               | 2.285714286       | 20             | 7               | 2.857142857       | 0.3293499                | 0.000266316         | 0.0071775                   | 6.4386    | 0.22413 | 0    | 0.22413 | 0.7  | 0.406739| 0.293261 |
| 3      | 20              | 7               | 2.857142857       | 24             | 7               | 3.428571429       | 0.3321692                | 0.000355            | 0.006576                    | 6.45614   | 0.228043| 0    | 0.228043| 0.7  | 0.410609| 0.289391 |
| 4      | 24              | 7               | 3.428571429       | 28             | 7               | 4                | 0.3341168                | 0.000420175         | 0.006729                    | 6.4386    | 0.231552| 0    | 0.231552| 0.7  | 0.412813| 0.287187 |
| 5      | 28              | 7               | 4                | 32             | 7               | 4.571428571       | 0.3355426                | 0.000485299         | 0.029133                    | 6.42553   | 0.232174| 0    | 0.232174| 0.7  | 0.414957| 0.285043 |
| 6      | 30              | 7               | 4.285714286       | 34             | 7               | 4.857142857       | 0.3361219                | 0.00051775          | 0.0323325                   | 6.43617   | 0.23366 | 0    | 0.23366 | 0.7  | 0.415917| 0.284083 |
| 7      | 32              | 7               | 4.571428571       | 36             | 7               | 5.142857143       | 0.3366323                | 0.000550227         | 0.00663                     | 6.42553   | 0.233913| 0    | 0.233913| 0.7  | 0.417391| 0.282609 |
| 8      | 34              | 7               | 4.857142857       | 38             | 7               | 5.428571429       | 0.3370865                | 0.0005853           | 0.028998                    | 6.4189    | 0.235652| 0    | 0.235652| 0.7  | 0.417913| 0.282087 |
| 9      | 36              | 7               | 5.142857143       | 40             | 7               | 5.714285714       | 0.3374919                | 0.0006156           | 0.0062995                   | 6.43509   | 0.23608 | 0    | 0.23608 | 0.7  | 0.417708| 0.282292 |
| 10     | 38              | 7               | 5.428571429       | 42             | 7               | 6                | 0.3378575                | 0.00064778          | 0.006712                    | 6.42105   | 0.236087| 0    | 0.236087| 0.7  | 0.419079| 0.280921 |
| 11     | 15              | 7               | 2.142857143       | 18             | 7               | 2.571428571       | 0.3321692                | 0.0002664           | 0.0069595                   | 6.4386    | 0.227913| 0    | 0.227913| 0.7  | 0.411111| 0.288889 |
| 12     | 17              | 7               | 2.428571429       | 24             | 7               | 3.428571429       | 0.3209757                | 0.000327018         | 0.0071195                   | 6.47368   | 0.211957| 0    | 0.211957| 0.7  | 0.395652| 0.304348 |
| 13     | 19              | 7               | 2.714285714       | 26             | 7               | 3.714285714       | 0.3231163                | 0.00036             | 0.0252075                   | 6.45614   | 0.215   | 0    | 0.215   | 0.7  | 0.397917| 0.302083 |
| 14     | 21              | 7               | 3                | 28             | 7               | 4                | 0.3249025                | 0.0003931           | 0.030673                    | 6.45614   | 0.217043| 0    | 0.217043| 0.7  | 0.400833| 0.299167 |
| 15     | 23              | 7               | 3.285714286       | 33             | 7               | 4.714285714       | 0.3198668                | 0.0004463           | 0.006933                    | 6.47368   | 0.210263| 0    | 0.210263| 0.7  | 0.393854| 0.306146 |
| 16     | 25              | 7               | 3.571428571       | 35             | 7               | 5                | 0.3215493                | 0.000479545         | 0.00691915                  | 6.45614   | 0.213043| 0    | 0.213043| 0.7  | 0.395906| 0.304094 |
| 17     | 27              | 7               | 3.857142857       | 37             | 7               | 5.285714286       | 0.3230187                | 0.0005122           | 0.006803                    | 6.456     | 0.215652| 0    | 0.215652| 0.7  | 0.397391| 0.302609 |
| 18     | 30              | 7               | 4.285714286       | 15             | 7               | 2.142857143       | 0.3918490                | 0.000320399         | 0.007206                    | 6.55682   | 0.314783| 0    | 0.314783| 0.7  | 0.49375 | 0.20625  |
| 19     | 33              | 7               | 4.714285714       | 17             | 7               | 2.428571429       | 0.3898867                | 0.000361            | 0.007375                    | 6.52273   | 0.3125  | 0    | 0.3125  | 0.7  | 0.491087| 0.208913 |
| 20 | 36 | 7 | 5.142857143 | 18 | 7 | 2.571428571 | 0.3918490 | 0.000574 | 0.00786 | 6.55625 | 0.321304| 0 | 0.321304| 0.7 | 0.49932 | 0.20068 |


# Propagation Delay (t_pd) in Inverter Characterization
Propagation delay (t_pd) is a critical parameter in digital circuits, particularly in the design and characterization of inverters. It refers to the time it takes for a change in the input signal to produce a corresponding change in the output signal. Understanding propagation delay is essential for ensuring that a circuit operates correctly at the desired frequency and meets timing specifications.
## Measuring Propagation Delay with Ngspice

To determine the propagation delay of an inverter using Ngspice, follow these steps:

1. **Circuit Setup:**
   - Create a netlist for the inverter circuit in Ngspice. This includes defining the inverter's Pfet and Nfet transistors and setting up the input and output connections.You can generate spice from the xschem with inverter_vtc_.sch
Generating a SPICE Netlist from Xschem

Follow these steps to generate a SPICE netlist from your schematic in Xschem:

- Step 1: Open Your Schematic
1. Launch Xschem.
2. Open your schematic file ( `inverter_vtc.sch`).

- Step 2: Set Up Netlist Generation
- Ensure your schematic is correctly configured with all components and connections.

- Step 3: Export the Netlist
1. Navigate to the menu bar.
2. Look for the option to generate or export a netlist. This is typically found under `File` or a specific `Export` menu.
3. Select "Export SPICE" or "Generate Netlist."

- Step 4: Choose the Format
- Choose the SPICE format (or any other format you need) and specify any necessary parameters.

- Step 5: Save the Netlist
- Select a destination to save the generated netlist file.

- Step 6: Run Simulation
- Use the generated netlist in your simulation software, such as Ngspice.

You have now successfully generated a SPICE netlist from your schematic in Xschem!
   

For performing the transient analysis, the following code is required:
```
v {xschem version=3.4.5 file_version=1.2
}
G {}
K {}
V {}
S {}
E {}
N 210 70 210 110 {
lab=nfet_out}
N 170 40 170 140 {
lab=nfet_in}
N 210 -40 210 10 {
lab=vdd}
N 210 170 210 220 {
lab=GND}
N 210 140 280 140 {
lab=GND}
N 280 140 280 200 {
lab=GND}
N 210 200 280 200 {
lab=GND}
N 210 40 300 40 {
lab=vdd}
N 300 -20 300 40 {
lab=vdd}
N 210 -20 300 -20 {
lab=vdd}
N 120 80 170 80 {
lab=nfet_in}
N 210 90 310 90 {
lab=nfet_out}
C {/home/dasari/Desktop/asap_7nm_Xschem/asap_7nm_pfet.sym} 190 40 0 0 {name=pfet1 model=asap_7nm_pfet spiceprefix=X l=7e-009 nfin=38}
C {/home/dasari/Desktop/asap_7nm_Xschem/asap_7nm_nfet.sym} 190 140 0 0 {name=nfet1 model=asap_7nm_nfet spiceprefix=X l=7e-009 nfin=42}
C {gnd.sym} 210 220 0 0 {name=l1 lab=GND}
C {lab_pin.sym} 210 -40 0 0 {name=p4 sig_type=std_logic lab=vdd}
C {lab_pin.sym} 120 80 0 0 {name=p5 sig_type=std_logic lab=nfet_in}
C {lab_pin.sym} 310 90 2 0 {name=p1 sig_type=std_logic lab=nfet_out}
C {vsource.sym} -80 100 0 0 {name=V1 value="pulse(0 0.7 20p 10p 10p 20p 500p 1)" savecurrent=false}
C {gnd.sym} -80 130 0 0 {name=l2 lab=GND}
C {lab_pin.sym} -80 70 0 0 {name=p2 sig_type=std_logic lab=nfet_in}
C {vsource.sym} 410 170 0 0 {name=V2 value=0.7 savecurrent=false}
C {gnd.sym} 410 200 0 0 {name=l3 lab=GND}
C {lab_pin.sym} 410 140 0 0 {name=p3 sig_type=std_logic lab=vdd}
C {code_shown.sym} 510 50 0 0 {name=s1 only_toplevel=false value="
.tran 0.1p 100p 
.control
    run
    set xbrushwidth=3
    plot  nfe_out nfet_in
.endc
"}
```
![image](https://github.com/user-attachments/assets/ee5c19c9-be7a-4a24-97a2-d0796111b250)
Figure snapshot of the xschem performing transient analysis
![image](https://github.com/user-attachments/assets/c26390c0-24db-468f-b0db-6849b9a725a6)
Figure snapshot of the output plot nfet_in vs nfet_out 

Calculating Rise Delay:
- Zoom In: Focus on the segment of the waveform where the input pulse transitions downward and the output pulse transitions upward, particularly around the voltage level of 50% = Vdd/2​​(0.35v). You can achieve this by right-clicking on the waveform and dragging to highlight the relevant area.
- Identify Points: Click on the rising edge of the output waveform at 50% = Vdd/2​​(0.35v) to note the coordinates (x0, y0).
- Find Input Point: Similarly, identify the corresponding point for the falling edge of the input waveform at 50% = Vdd/2​​(0.35v).

- Calculate Delay: The rise delay is then calculated by finding the difference between the x-coordinate of the output's rising edge and the x-coordinate of the input's falling edge.

Calculating Fall Delay:
- Zoom In: Focus on the section of the waveforms where the input pulse rises and the output pulse falls, especially near the voltage level of 50% = Vdd/2​​(0.35v). Right-click and drag to select this area.
- Identify Points: Click on the falling edge of the output waveform at 50% = Vdd/2​​(0.35v) to obtain the coordinates (x0, y0).
- Find Input Point: Next, locate the corresponding point for the rising edge of the input waveform at 50% = Vdd/2​​(0.35v).
- Calculate Delay: The fall delay is determined by subtracting the x-coordinate of the input's rising edge from the x-coordinate of the output's falling edge.

![image](https://github.com/user-attachments/assets/22653a1f-8d9f-43dd-9ed1-d3653b0ef799)




