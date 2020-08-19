# Sample code with examples to simplify connection to Cobolt Lasers
[ ![Build Status](https://travis-ci.com/cobolt-lasers/samples.svg?branch=master)](https://travis-ci.com/cobolt-lasers/samples)  (Linux) 

## hello_laser
The program hello_laser, demonstrates how to enumerate system COM ports, choose the port corresponding to a Cobolt laser and then fetches the serial number of that laser.

The program is currently written for C++ and Python.

### Python
#### Dependencies
The python version requires Python 3 and pyserial, [Pyserial](https://pypi.org/project/pyserial/).

#### Target Platforms
Any platform that Python and Pyserial supports.

Installation of pyserial:

Open a terminal ( Command Handler / Powershell / Bash ).
```
python -m pip install pyserial
```

### C++
#### Dependencies
The C++ version depends on a cross platform COM-port library [wjwwood-serial](https://github.com/wjwwood/serial). A copy is already included in this repo.

#### Target Platforms
It should supports any platform that wjwwood-serial support:
  * Windows
  * Linux
  * osx
The c++ version is however developed on Windows but built on TravisCI to verify compilation on various targets. 

#### Building the program
The program is built using [cmake](https://cmake.org/), a build-system that is integrated in Visual Studio 2017+.

#### C++ in Visual Studio 2017+
1. Start Visual Studio
2. Select File->Open Folder
3. Select samples/cpp

Intellisense will parse the CMakeLists.txt file and hello_laser.exe will appear as a build target by the green arrow.

#### In any terminal
cmake can also be run in any terminal:
```
cmake -S PATH/CMakeLists.txt -B build/
```
See cmake -help for more information on selecting build tools.








