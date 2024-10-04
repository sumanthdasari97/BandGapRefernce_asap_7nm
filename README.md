# BandGapRefernce_asap_7nm

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

| Sr. No | W (Width) PMOS | L (Length) PMOS | (W/L Ratio) PMOS | W (Width) NMOS | L (Length) NMOS | (W/L Ratio) NMOS | Threshold Voltage (Vth) |
|--------|-----------------|-----------------|------------------|----------------|-----------------|------------------|-------------------------|
| 1      | 14              | 7               | 2                | 14             | 7               | 2                | 0.3447862                |
| 2      | 16              | 7               | 2.285714286       | 20             | 7               | 2.857142857       | 0.3293499                |
| 3      | 20              | 7               | 2.857142857       | 24             | 7               | 3.428571429       | 0.3321692                |
| 4      | 24              | 7               | 3.428571429       | 28             | 7               | 4                | 0.3341168                |
| 5      | 28              | 7               | 4                | 32             | 7               | 4.571428571       | 0.3355426                |
| 6      | 30              | 7               | 4.285714286       | 34             | 7               | 4.857142857       | 0.3361219                |
| 7      | 32              | 7               | 4.571428571       | 36             | 7               | 5.142857143       | 0.3366323                |
| 8      | 34              | 7               | 4.857142857       | 38             | 7               | 5.428571429       | 0.3370865                |
| 9      | 36              | 7               | 5.142857143       | 40             | 7               | 5.714285714       | 0.3374919                |
| 10     | 38              | 7               | 5.428571429       | 42             | 7               | 6                | 0.3378575                |
| 11     | 15              | 7               | 2.142857143       | 18             | 7               | 2.571428571       | 0.3321692                |
| 12     | 17              | 7               | 2.428571429       | 24             | 7               | 3.428571429       | 0.3209757                |
| 13     | 19              | 7               | 2.714285714       | 26             | 7               | 3.714285714       | 0.3231163                |
| 14     | 21              | 7               | 3                | 28             | 7               | 4                | 0.3249025                |
| 15     | 23              | 7               | 3.285714286       | 33             | 7               | 4.714285714       | 0.3198668                |
| 16     | 25              | 7               | 3.571428571       | 35             | 7               | 5                | 0.3215493                |
| 17     | 27              | 7               | 3.857142857       | 37             | 7               | 5.285714286       | 0.3230187                |
| 18     | 30              | 7               | 4.285714286       | 15             | 7               | 2.142857143       | 0.3918490                |
| 19     | 33              | 7               | 4.714285714       | 17             | 7               | 2.428571429       | 0.3898867                |
| 20     | 36              | 7               | 5.142857143       | 18             | 7               | 2.571428571       | 0.3918490                |


