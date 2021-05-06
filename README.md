# HexConv
## ABOUT
A BASH script designed to take a hexadecimal string as an input value and convert it into various other formats, including; ASCII, Binary, Decimal, etc.

Since delving into the world of reverse-engineering, I have been playing around a lot recently with a disassembly tool called `radare2`. Throughout this learning process, I have written basic `C` programs to aid with understanding how to disassemble the resulting compiled binary.

One of the programs I wrote was simply a series of variables, initalised with varying values. One of these values was a floating-point number specified as a 'double' data-type. Upon disassembling the binary, I found that a hexadecimal value was being pushed into the register corresponding with this variable. However, I was unsure how to interpret the hexadecimal value.

Thus began my research into the fascinating mathematics behind floating-point binary numbers. Wherein I discovered how to manually convert a given 32-bit (Short Real) or 64-bit (Long Real) hexadecimal string into a floating-point number.

As always, I decided to conclude my research by creating a script to do this conversion for me. To which I chose BASH, since I predominantly work on Linux systems and I believed it would provide an interesting challenge.

Interestingly, I had created a Hexadecimal-Converter BASH script some years ago, which was very basic and only converted a given string into ASCII, Binary and Decimal. I was able to re-purpose some of its code into the BASH script outlined below. To make things extra challenging for myself, I decided to use pure BASH logic and remove any reliance on external tools such as `bc`.

## USAGE

```shell
$   ./hexconv [-arg/--argument] [HEXADECIMAL STRING]
```

## ARGUMENTS

* `-a`, `--ascii`:    Convert a hexadecimal string into ASCII
* `-b`, `--binary`:   Convert a hexadecimal string into Binary
* `-c`, `--convert`:  Convert a hexadecimal string into ASCII, Binary and Decimal
* `-d`, `--decimal`:  Convert a hexadecimal string into Decimal
* `-fh`, `--floath`:  Convert a 16-bit hexadecimal string into a Floating-Point number
* `-fs`, `--floats`:  Convert a 32-bit hexadecimal string into a Floating-Point number
* `-fd`, `--floatd`:  Convert a 64-bit hexadecimal string into a Floating-Point number
* `-fq`, `--floatq`:  Convert a 128-bit hexadecimal strint into a Floating-Point number
* `-v`, `--version`:  Display version number and exit
* `-h`, `--help`:     Display help information and exit

Please ensure that the hexadecimal string being converted is used as the second argument of the command-line and contains ONLY valid hexadecimal characters (not including `0x` characters). The first argument of the command-line will determine what the input string is to be converted into.

This script currently supports converting hexadecimal strings into the following formats:

* ASCII
* Binary (Base 2)
* Decimal (Base 10)
* Floating-Point (Half / Single / Double & Quadruple precision values)

## EXAMPLES

Convert a hexadecimal string into binary:
```shell
$   ./hexconv -b 040b18
```

Convert a hexadecimal string into ASCII, Binary and Decimal:
```shell
$   ./hexconv -c 55aa
```

Convert a hexadecimal string into a single precision floating-point value:
```shell
$   ./hexconv -fs 40db3333
```

Display help information and exit the tool:
```shell
$   ./hexconv --help
```

## CHANGELOG

* v1.00 (2017-07-15):  An old script I had written to do basic hexadecimal conversions. This script was used as a rough template.
* v2.00 (2021-05-03):  Re-wrote the conversion logic from the old script to rely less on external tools such as `bc` and streamlined the code.
* v2.02 (2021-05-03):  Added much more sanitisation to ensure that the output remains clean and user-readable.
* v2.03 (2021-05-03):  Hotfix for a logic error I overlooked when converting to ASCII.
* v2.04 (2021-05-03):  Implemented a function for converting a 32-bit hexadecimal string to a single precision floating-point number.
* v2.05 (2021-05-03):  Further testing conducted on the floating point conversion. Altered some of the logic to remain consistent when dealing with negative numbers.
* v2.06 (2021-05-04):  Implemented logic for 64-bit and 128-bit conversions into their respective floating-point value. Tested and are working properly.
* v2.07 (2021-05-04):  Implemented logic for 16-bit conversions into half-precision floating-point numbers.
* v2.50 (2021-05-04):  Fixed multiple errors with null bytes. Fixed an issue with the calculation of floating numbers where the exponent was all 0s. Implemented and tested new scripts for handling ASCII conversions. Made various improvements to the code and removed many repeated lines.
* v2.60 (2021-05-05):  Completely reworked the logic used to calculate floating point values. Added more precision to the output of floating point numbers using `awk`. All tested and converting as intended.
* v2.61 (2021-05-05):  Hotfix for an error which was thrown when a single argument was supplied to the script.    

## KNOWN ISSUES / FUTURE CHANGES  

There are issues in the ASCII conversion when handling NULL bytes (Caused by how BASH handles parameters as C-strings). I have tried to account for this as much as possible in the code.

This script is currently only capable of handling 16-bit, 32-bit, 64-bit and 128-bit hexadecimal values for conversion into floating-point numbers. Logic supporting 8-bit (or other) values might be implemented in a future revision.
