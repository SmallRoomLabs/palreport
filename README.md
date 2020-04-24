# palreport ![C/C++ CI](https://github.com/SmallRoomLabs/palreport/workflows/C/C++%20CI/badge.svg)
Lists sizes of the functions in a listing file from Palbart (PDP-8)

## Usage
Each function in the source needs to have its start and end marked by a
comment line.  The start marker is /[ and the end marker is /]

As can be seen in the example below it is rather unintrusive in the code:

```
//
// Output the data in AC to the TTY and wait for the TTY
// to become ready again. Clears AC and L before returning
//
// Inputs: 	AC
// Modifies: 	AC,L
/[
ChrOut,	0 
	TLS		/ Send to TTY
	TSF		/ Wait for TTY to become ready
	JMP	.-1
	CLA CLL		/ Clear AC and L
	JMP I	ChrOut
/]
```

To run the script just pipe in the XXX.lst -file generated by palbar into
the script like `./palreport.sh < mycode.lst`

## Sample output

The output looks like this. Each line has the starting address of the
function, followed by the function name and the length in (decimal) of the
function. If there's some unused space between this function and the next
that will be reported as "..followed by..."

```
0400  ATOL     39 bytes
0450  CpyBlk   21 bytes
0476  ReadLi   50 bytes followed by 15 unused bytes
0600  GetKey    7 bytes
0610  FndLin    1 bytes
0612  TxtOut   11 bytes
0626  DigOut    3 bytes
0632  ChrOut    5 bytes followed by 96 unused bytes
1000  DMUL    121 bytes followed by 6 unused bytes
1200  DIVIDE   61 bytes followed by 66 unused bytes
1400  Tokeni   81 bytes
1522  AppDst    5 bytes followed by 40 unused bytes
1600  ZeroM     5 bytes
1606  SkipSp   10 bytes
1621  IncSrc    5 bytes
1627  Syntax    2 bytes
1632  List     84 bytes followed by 157 unused bytes
2214  Greet   152 bytes
```