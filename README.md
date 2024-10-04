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

