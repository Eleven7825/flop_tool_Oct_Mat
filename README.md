# flopTool
Flop counter in Matlab/Octave

## Author
Leonardo T. Rolla and Shiyi Chen

## License
GNU Lesser General Public License, either version 3 of the License, or any later version.

## Discription
This tool evaluates the complexity of a given M script by counting its flops. Flops represent for floating-point operations. Some flops for operations are listed below:
Operation | Dimension | Flops
---------|----------|--------------
`a * x` | `a` is a scalar, `x` is a n by 1 array | `n` 
`x * y` | `x` and `y` are both n by 1 arrays | `2n` 
`A * x` | `A` is m by n array, `x` is n by 1 array | `2*m*n`
`A * B` | `A` is m by r array, `B` is r by n array | `2*m*n*r`
`A .* B` | `A` and `B` are both m by n arrays | `2*m*n` 
`A + B` | `A` and `B` are both m by n arrays | `m*n` 
`A - B` | `A` and `B` are both m by n arrays | `m*n`
`A/ b` | `A` is m by m array, `b` is m by 1 array | about `(2*m^3)/3`

## Usage
Run `easy_runtest.m` for the usage guidance.

## Warnings

Notice the command window, if the program terminates without any output in command window, then there will be a temporary file called `fileName_tmp.m` generated under the same folder. If warning appears, the program will tell the user which line in the original file causes the problem. The user needs to check the line in the original file and fixes the error. There are two types of warning:

1. `Warning: In line XX, unrecognized pattern`indicates the flop analyzer crashed at XX line. For example, there may be some brackets missing which caused the program fail to read the variables. In this case, the program will jump it and continue counting the rest of script. The user needs to check whether the brackets are missing in the line, then run `flop_script.m` again.

1. `Warning: In line XX, can't find left variable, assigning value 1 to it`, in this case, program does not find variables corresponding to operators in this line. The program will automatically assign 1 to that unknown variable and continue counting in this line. The user need to add brackets around the variable they want the program to count at the original file and run `flop_script.m` again, the temporary file will be automatically overwritten if the user run it again.

## Comparison
We want users to have a choice between our tool and former tool writen by [Qian Hang](http://hangqian.weebly.com/)(his work can be find [here](https://www.mathworks.com/matlabcentral/fileexchange/50608-counting-the-floating-point-operations-flops)).

flopTool |  FLOPS
-------------|--------------
Compatible with GNU Octave and Matlab. | Only for Matlab.
"flopTool" may be more convenient for counting with changing input variable sizes in the sense that it does not need profiling, saving or loading MAT files. | Need profiling, saving and loading MAT files.
Longer elapse time for the temporary counting tool, which makes our tool not suitable for a long script. | Same elapse time with the original file.
Cannot recognize functions containing multiple arguments. | Can accept some multiple arguments like sum(A,2). 
Cannot recognize functions handles. | Can recognize bsxfun. 
Cannot know exact flops in each line.  | Display flops at each line and their executed rounds. 
Support variable changes and slicing. | Does not support variable changes and slicing. 
Support sparse matrices.  | Does not support sparse matrices.
Support multiple functions in a script but not nested. | Support nested function.
Change the rules in TXT file. | Change the rules in EXCEL file.
Support Octave > 4.2.0 and Matlab. | Only support Matlab.
Generate transparent code in a separate M file for auditing. | Display the flop count on the command window for auditing.
