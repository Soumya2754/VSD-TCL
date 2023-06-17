# VSD-TCL
# A repository for documentation of VSD-TCL workshop

_Author: Soumya Kulhalli_

_Acknowledgments: TCL Workshop of VlSI System Design by Kunal Ghosh_

# Task: Write a TCL program which reads parameters from an excel sheet and performs Synthesis and STA analysis and display the timing results as a datasheet
_Synthesis will be performed using Yosys_ 

 _STA analysis using OpenTimer_

Progress Quick-Link:<br />
[Day 1](#Day_1)<br />
[Day 2](#Day_2)<br />


## Day_1

### Introduction to TCL 

_Sub Tasks:_

- Create a command to pass the .csv(excel sheet) from Unix Shell to TCL script
- Convert all inputs to format[1] and SDC format and pass it to synthesis tool 'Yosys'
- Convert format[1] and SDC to format[2] and pass it to timing tool 'OpenTimer'
- Generate the output timing report

**To create the command to pass .csv from UNIX shell to TCL script** 
Scenarios:
- no .csv provided
~~~
$argv[1]           // gives the first argument 
$argv[2]           // gives the second argument and so on....
$#argv             // gives the number of arguments passed in the command
~~~

to display an error message the following code snip can be used:
~~~
if($#argv != 1) then
echo "Please provide the .csv file only"
exit 1 
endif
~~~
save the file with the name vsdsynth and make it executable by executing the following command in the terminal:
~~~
sudo chmod -R 777 vsdsynth
~~~
 to execute the file use the following command:
 ~~~
 ./vsdsynth
~~~
- non-existent .csv provided and -help
The following code snip can be used:
~~~
if(! -f $argv[1] || $argv[1] == "-help") then
	if($argv[1] != "-help") then
		echo "Error: Cannot find csv file $argv[1]. Exiting..."
		exit 1
	else
		echo "USAGE: ./vsdsynth <csv file> , where the <csv file> consists of 2 columns  -->  1st column is being case sensitive."
		echo "Note if the file is not in the same directory, ensure to include the path along with the <csv file>"
		echo 
		echo "<Design Name> is the name of the top module"
		echo 
		echo "<Output Directory> is the name of the output directory where you want to dump synthesis script, synthesized netlist and timing report" 
		echo 
		echo "<Netlist Directory> is the name of the directory where all RTL netlist are present"
		echo
		echo "<Early Library Path> is the file path of the early cell library to be used for STA"
		echo
		echo "<Late Library Path> is the file path of the late cell library to be used for STA"
		echo
		echo "<Constratints file> is the csv file path of constraints to be used for STA"
		echo
		exit 1
	endif
else
		tclsh vsdsynth.tcl $argv[1]
endif
~~~

Explanation:
~~~
-f $argv[1]      //gives a 1 if the file exists in the pwd
~~~
![Screenshot from 2023-06-14 19-32-37](https://github.com/Soumya2754/VSD-TCL/assets/83526493/023bdfed-3e08-47b7-b3c2-194f731123e6)

## Day_2

Notes:
~~~ 
puts "prints the text on terminal"
file isdirectory <directory_path>       //returns 1 if directory exists 
~~~
