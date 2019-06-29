<!--
    Licensed to the Apache Software Foundation (ASF) under one
    or more contributor license agreements.  See the NOTICE file
    distributed with this work for additional information
    regarding copyright ownership.  The ASF licenses this file
    to you under the Apache License, Version 2.0 (the
    "License"); you may not use this file except in compliance
    with the License.  You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing,
    software distributed under the License is distributed on an
    "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
    KIND, either express or implied.  See the License for the
    specific language governing permissions and limitations
    under the License.
-->

# AMCL - *Apache Milagro Crypto Library*

[![Master Branch](https://img.shields.io/badge/-master:-gray.svg)](https://github.com/apache/incubator-milagro-crypto-c/tree/master)
[![Master Build Status](https://travis-ci.org/apache/incubator-milagro-crypto-c.svg?branch=master)](https://travis-ci.org/apache/incubator-milagro-crypto-c)
[![Master Coverage Status](https://coveralls.io/repos/github/apache/incubator-milagro-crypto-c/badge.svg?branch=master)](https://coveralls.io/github/apache/incubator-milagro-crypto-c?branch=master)

[![Develop Branch](https://img.shields.io/badge/-develop:-gray.svg)](https://github.com/apache/incubator-milagro-crypto-c/tree/develop)
[![Develop Build Status](https://travis-ci.org/apache/incubator-milagro-crypto-c.svg?branch=develop)](https://travis-ci.org/apache/incubator-milagro-crypto-c)
[![Develop Coverage Status](https://coveralls.io/repos/github/apache/incubator-milagro-crypto-c/badge.svg?branch=develop)](https://coveralls.io/github/apache/incubator-milagro-crypto-c?branch=develop)

* **category**:    Library
* **copyright**:   2019 The Apache Software Foundation
* **license**:     ASL 2.0 ([Apache License Version 2.0, January 2004](http://www.apache.org/licenses/LICENSE-2.0))
* **link**:        https://github.com/apache/incubator-milagro-crypto-c

## Description

*AMCL - Apache Milagro Crypto Library*

AMCL is a standards compliant C cryptographic library with no external dependencies.

AMCL is provided in *C* language but includes a *[Python](https://www.python.org)* wrapper for some modules to aid development work.

NOTE: This product includes software developed at *[The Apache Software Foundation](http://www.apache.org/)*.

## Software Dependencies

In order to build this library, the following packages are required:

* [CMake](https://cmake.org/) is required to build the source code.
* [CFFI](https://cffi.readthedocs.org/en/release-0.8/), the C Foreign Function Interface for Python is required in order to execute tests.
* [Doxygen](http://doxygen.org) is required to build the source code documentation.
* [Python](https://www.python.org/) language is required to build the Python language wrapper.


The above packages can be installed in different ways, depending on the Operating System used:

* **Debian/Ubuntu Linux**


    sudo apt-get install -y git cmake build-essential python python-dev python-pip libffi-dev doxygen doxygen-latex parallel
    sudo pip install cffi


* **RedHat/CentOS/Fedora Linux**

```
sudo yum groupinstall "Development Tools" "Development Libraries"
sudo yum install -y git cmake python libpython-devel python-pip libffi-devel doxygen doxygen-latex parallel
sudo pip install cffi
```

* **MacOS**

```
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew install cmake
brew install pkg-config libffi
sudo pip install cffi
brew install doxygen
brew install parallel
```

* **Windows**
* Minimalist GNU for Windows [MinGW](http://www.mingw.org) provides the tool set used to build the library and should be installed
* When the MinGW installer starts select the **mingw32-base** and **mingw32-gcc-g++** components
* From the menu select *"Installation"* &rarr; *"Apply Changes"*, then click *"Apply"*
* Finally add *C:\MinGW\bin* to the PATH variable
* pip install cffi
* install CMake following the instructions on http://www.cmake.org
* install Doxygen following the instructions on http://www.doxygen.org


## Build Instructions

#### Linux and Mac

##### Quick start

A Makefile is present at the project root that reads the options defined in
config.mk. Change these options and then type the following to build and test
the library.

```
make
```

##### Multiple curves and RSA security levels

The default build (see config.mk) uses multiple curves and RSA security
levels. There is an example called testall.c in the examples directory that
shows how to write a program to use the different curves etc in a single
program. To build and run the example use this script;

```
./scripts/buildMulti.sh
```

##### Manual build

NOTE: The default build is for 64 bit machines

```
git clone https://github.com/milagro-crypto/milagro-crypto-c
cd milagro-crypto-c
mkdir -p target/build
cd target/build
cmake ../..
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:./
make
make test
make doc
sudo make install
```

On Debian/Ubuntu machine instead of executing the *"sudo make install"* command it is possible to execute *"sudo checkinstall"* to build and install a DEB package.

Now you can set the path to where libs and python package are installed:

```
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:./:/opt/amcl/lib
export PYTHONPATH=/usr/lib/python2.7/dist-packages
```

NOTE: The build can be configured by setting flags on the command line, for example:

```
cmake -DAMCL_CHUNK=64 ../..
cmake -D CMAKE_INSTALL_PREFIX=/opt/amcl -D AMCL_CHUNK=64 -D BUILD_WCC=on ../..
```

It is possible also to build the library supporting more than one elliptic curve and more  than one RSA security level, for example

```
cmake -DAMCL_CURVE=BN254CX,NIST254 -DAMCL_RSA=2048,3072 ../..
```

To list other available CMake options, use:

```
cmake -LH
```

##### Uninstall software

```
sudo make uninstall
```

##### Building an installer

After having built the libraries you can build a binary installer and a source distribution by running this command

```
make package
```

#### Windows

Start a command prompt as an administrator

```
git clone https://github.com/milagro-crypto/milagro-crypto-c
cd milagro-crypto-c
mkdir target\build
cd target\build
cmake -G "MinGW Makefiles" ..\..
mingw32-make
mingw32-make test
mingw32-make doc
mingw32-make install
```

Post install append the PATH system variable to point to the install ./lib:

*My Computer -> Properties -> Advanced > Environment Variables*

The build can be configured using by setting flags on the command line i.e.

```
cmake -G "MinGW Makefiles" -D BUILD_PYTHON=on ..
```

##### Uninstall software

```
mingw32-make uninstall
```

##### Building an installer

After having built the libraries you can build a Windows installer using this command

```
sudo mingw32-make package
```

In order for this to work NSSI has to have been installed

## Contributions

This project includes a Makefile that allows you to test and build the project in a Linux-compatible system with simple commands.
All the artifacts and reports produced using this Makefile are stored in the *target* folder.

All the packages listed in the *Dockerfile* are required in order to build and test all the library options in the current environment. Alternatively, everything can be built inside a [Docker](https://www.docker.com) container using the command "make -f Makefile.docker buildall".

To see all available options:

```
make help
```

To build the builder Docker image:

```
make -f Makefile.docker
```

To build the project inside a Docker container (requires Docker) you need to build a builder image (once), and then build the project in its context:

```
make -f Makefile.docker buildall
```

To build a particular set of predefined makefile options inside a Docker container:

```
make -f Makefile.docker build TYPE=LINUX_64BIT_NIST256_RSA2048
```

or in the current environment:

```
make build TYPE=LINUX_64BIT_NIST256_RSA2048
```

To execute all the test builds and generate reports in the current environment:
```
make qa
```

To format the code (please use this command before submitting any pull request):
```
make format
```
### Contributors 

The following people have contributed to milagro-crypto-c

- Mike Scott
- Kealan McCusker
- Alessandro Budroni
- Samuele Andreoli

Please add yourself here if you make or have made a contribution.

### Making a Contribution

1.  [Check for open issues](https://github.com/apache/incubator-milagro-crypto-c/issues) or start a discussion around a feature idea or a bug by sending a mail to dev@milagro.incubator.apache.org
2.  Fork the repository to start making your changes. Please use the "development" branch as a basis.
3.  Write a test which shows that the bug was fixed or that the feature works as expected.
4.  Make a pull request with a reference to the issue


## Crypto Notice

This distribution includes cryptographic software. The country in which you
currently reside may have restrictions on the import, possession, use, and/or
re-export to another country, of encryption software. BEFORE using any
encryption software, please check your country's laws, regulations and
policies concerning the import, possession, or use, and re-export of encryption
software, to see if this is permitted. See <http://www.wassenaar.org/> for
more information.

The Apache Software Foundation has classified this software as Export Commodity
Control Number (ECCN) 5D002, which includes information security software using
or performing cryptographic functions with asymmetric algorithms. The form and
manner of this Apache Software Foundation distribution makes it eligible for
export under the "publicly available" Section 742.15(b) exemption (see the BIS
Export Administration Regulations, Section 742.15(b)) for both object code and
source code.


