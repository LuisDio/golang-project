# golang-project

## Golang installation and Setup for macOs

First, download the latest 64 bit macOs package from the download page. 

When you install Go on your system, it creates a directory /usr/local/go in UNIX or c:/go in Windows. Then it copies all necessary code and binaries needed for Go to function in this directory.

***Generally, you don’t need to setup GOROOT environment variable. I recommend not to modify/use GOROOT variable anywhere unless it is absolutely necessary.***

**```$GOROOT/src```**  is the direcory where packages are found such the **Standard Library package** <br/>
If package is not present there, then Go refers to system's environment variable ```GOPATH```.<br>

**```$GOPATH```** is the path to the GO workspace directory which contains all the written source code and ```$GOPATH/src``` is the path to the package within the workspace. Basically this is where you may store store your package. <br/>

You can have as many workspace as you want, as long you keep ```$GOPATH```environment variable pointed to the current working space directory. <br/>


## The Workspace directory structure

A Go workspace directory must have ***three sub directories***. ```src```, ```pkg``` and ```bin```. 

If you want to setup Go workspace, follow this **documentation**. If you are using MacOS, the you can follow this Medium **article** to setup environment variables both temporarily or permanently.<br/>

- src <br/>
**src** directory contains GO packages. Any packages installed using ```go get```command will reside here as well.<br/>
In GO, every program is contained in a package. Hence, whenever you will be working with new Go project, you need to create new directory inside $GOPATH/src

- pkg <br/>
**pkg** directory contains Go package objects. They are compiled version of original package source code and they have .a file extension (a stands for archived).<br/>
These files contain the compiled package binary code, along with debug symbols and source information. A package object is customized for machine architecture and Go version. These files are created by the Go pack tool while building/installing a package.

- bin <br/>
A Go program can either be meant to used as utility inside a package or to perform some operation. We have seen packages and where they reside.<br/>
A Go program which is meant to perform some operation like make a **network request** or **write something to a file** needs to be compiled first, so that your machine can understand the instructions. When you run ```go run hello.go``` command, Go compiler first compiled hello.go file and then executes the resultant binary code.

You can output a binary file from a Go program or package using ```go build <package-name>``` (main package) or ```go build program/path.go``` command. This will create a binary file in current directory.

**bin** directory contains same binary executable files. These files are creating by go install commands. go install command runs go build command internally and output theses files to bin directory. Generally, this directory is in the executable path of the system. Hence all the programs inside this directory is executable from the terminal.


## 1. Setup your environment variable
```
export GOPATH=/home/$USER/go_workspaces/main
export GOBIN=$GOPATH/bin

PATH=$PATH:$GOPATH:$GOBIN
export PATH
```
Setting ```GOBIN``` environment variable is not necessary, but since bin directory of a workspace will be in our PATH, it’s good idea set it for simplicity.

## 2. Make sure, $GOPATH and $GOBIN is set
```
>echo $GOROOT
>echo $GOPATH
>echo $GOBIN
```
There is no need to set GOROOT environment variables as we are using default installation directory

## 3. Installing 3rd party package
```
go get github.com/jinzhu/gorm
```
This command will pull source from GitHub repository and put it inside $GOPATH/src. This will also download other dependency packages of gorm and install under src directory.

You will obtain the follow directory structure <br/>

![dir-struc](https://raw.githubusercontent.com/LuisDio/golang-project/master/images/dir-struct.png)

After package and dependencies are downloaded, Go will compile package and create single package object file in $GOPATH/pkg directory under same directory structure of package.

## 4. Create binaries

Create a folder **shape** within the src folder. add a **main.go** and put the code below.
```
package main

import "fmt"

func main(){
  fmt.Println("Hello Go")
}
```
Then run the command
```
>go install shape
>shape
```
You will obtain such a directory struct

![dir-struc](https://raw.githubusercontent.com/LuisDio/golang-project/master/images/dir-struct1.png)


It doesn’t matter, from where you execute ```go install shape``` command, Go knows where shape package is (from **GOPATH** environment variable). Hence, a binary file is generate inside bin directory. <br/>
Since, this bin directory is in our PATH, we can execute these binary file just by it’s filename as command.









