# cxform
CXFORM: Coordinate transformation package for IDL and C with updated IGRF 12 coefficients 

# original source
https://spdf.sci.gsfc.nasa.gov/pub/software/old/selected_software_from_nssdc/coordinate_transform/

# compile the sample main-cli to use cxform from the command line interface
## firstly, compile the cxform shared library
```bash
conqueror@dev01:~/cxform$ make so-c
OS type detected: Linux
make[1]: Entering directory '/home/conqueror/cxform'
cc -fPIC -shared   -c -o cxform-auto.o cxform-auto.c
cc -fPIC -shared   -c -o cxform-manual.o cxform-manual.c
ld -G -lm -o cxform-c.so cxform-auto.o cxform-manual.o
make[1]: Leaving directory '/home/conqueror/cxform'
```

## only after that compile the main-customized-dt
```bash
conqueror@dev01:~/cxform$ make main-cli
ld -G -lm -o cxform-c.so cxform-auto.o cxform-manual.o
cc    -c -o main-cli.o main-cli.c
gcc ./cxform-c.so main-cli.o -lm -o main-cli
```
## usage (date time values must be provided without a leading zero)
```bash
conqueror@dev01:~/cxform$ ./main-cli 2017 04 19 1 48 0 11.111111 22.222222 33.333333
Time: 2017/04/19 01:48:00  (JD 2457862.575000, ES: 545838480)

Input Vector (J2000):   11.111111 22.222222 33.333333
Output Vector (GEO):  -24.551739  -3.967237 33.314684
Output Vector (GSE):  26.106872 23.989126 21.710553
Output Vector (GSM):  26.106872 11.185162 30.359816
Output Vector (SM): 23.742015 11.185162 32.242889
```
