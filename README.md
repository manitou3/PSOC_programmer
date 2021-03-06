##PSOC_programmer

#####Summary
Open source Unix tools to manipulate hex files and program a PSoC5 (ARM) via FX2 USB interface.

#####Purpose
* Tools to manipulate Intel hex files
* Configure the FX2 USB interface on the CY8CKIT.
* Program a hex file into a PSoC5 (ARM).


#####Requirements
* A Cypress CY8CKIT-050 dev kit, however some of the tools are of more general use.
* Developed on OS X, however it is expected to run under Linux (not yet tested)

#####See Also
* https://github.com/kiml/PSOC_compiler.git
* http://dfusion.com.au/wiki/  The ARM Embedded pages:
    - PSoC5 bare metal
    - PSoC5 programmer 
    - GCC Linker

#####Additional Uses
* A useful general purpose Intel hex manipulation library (libhex)

#####License
* All code is released under GPL v3 except for:
  -  libini a the third party library that is released with changes under its original New BSD license.

#####Raison d'Etre
* Cypress put out a free but closed source MS Windows development environment. They do provide GCC but pretty much everything else is proprietary which is fine but:
  - I like the PSoC feature set (basically ARM CPU, mxied signal FPGA, decent analogue)
  - I wanted to learn more about internals of the ARM Cortex M3 chip used
  - I wanted to program the PSoC under Unix.

Short version - the mountain was there so I climbed it :-)

#####Tools

`prog CMD`
  Talk to a PSoC ARM device. CMD is:
```
    program    filename   - program device
    upload     filename   - read device and save in file
    verify     filename   - verify device
    reset                 - reset device
    erase                 - erase device
    id                    - get jtag id
    usb_clear             - clear USB error on device
    help                  - display help
```

`hex2bin infile.hex outfile.bin`
  Converts intel hex files into binary files (note binary files may be quite large)

`hexinfo filename.hex`
  Dumps PSoC specific hex file into something slighly more readable.

```
   mergehex (-[cdemnp] infile.hex)+ [-o outfile.hex]
   mergehex (-[cdemnp] infile.hex)+ > outfile.hex
   Eg:  mergehex -c infile.hex -nm config.hex > outfile.hex
```
  Merge a newly compiled .hex program file with additional PSoC specific .hex
  configuration info to create a programmable hex file.
  This is an interim tool - ideally the additional configuration info comes
  from human readable config files rather than .hex snippets.

`freehex2other[.py] [-h] -f OUTPUT_FORMAT [-i INFILE] [-o OUTFILE]`
  Convert ASCII hex bytes to other formats

  optional arguments:
  -h, --help        show this help message and exit
  -f OUTPUT_FORMAT  output format: hex,intelhex,binary
  -i INFILE         input file. Default stdin
  -o OUTFILE        output file. Default stdout


`gen_config[.py] [-h] -f OUTPUT_FORMAT [-i INFILE] [-o OUTFILE]`
  Compile config data into freehex file format

  optional arguments:
  -h, --help  show this help message and exit
  -i INFILE   input file
  -o OUTFILE  output file. Default stdout

