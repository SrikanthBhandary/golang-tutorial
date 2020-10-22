# Learn GoLang #
Welcome to the quick tutorial on golang basics. Topics covered here are for the absolute beginners.  Intermediate or professional ones can also make use of it. Unlike other tutorials, we are not going to start with the legacy hello world program. We will start something with something advanced. Saying that, let's get started!

Let's start with the basics:

## Package: ##

In the most basic terms, A package is nothing but a directory inside your Go workspace containing one or more Go source files, or other Go packages. Every Go source file belongs to a package. In Go programming, the main package is present on the top of the program. This is because, the main package informs the go build that it must activate the linker to make an executable file. In Go language, package declaration is always present at the beginning of the source file and the purpose of this declaration is to determine the default identifier for that package when it is imported by another package. For example:

```package main```

The import declaration immediately comes after the package declaration. The Go source file contains zero or more import declaration and each import declaration specifies the path of one or more packages in the parentheses. With the help of an import path, you can import packages in your program. For example:

```
import "fmt"
```
Above statement will imoprt the single package. If you want to import multiple packages, then you can club all the imports in a following way.

```
import(
    "fmt"
    "strings"
    "bytes"
) 
```

In Go language, you are allowed to create a package inside another package simply by creating a subdirectory. And the nested package can import just like the root package. For example:

 ```import "math/cmplx"```

 Here, the math package is the main package and cmplx package is the nested package. Sometimes, some package may have the same names, but the path of the such packages are always different. For example, both math and crypto packages contain a **rand** named package, but the path of this package is different, i.e, math/rand and crypto/rand.


This **import** statement states that you are importing an **fmt** package in your program. The import path of packages is globally unique. To avoid conflict between the path of the packages other than the standard library, the package path should start with the internet domain name of the organization that owns or host the package. 

``` import "github.com/abc/xyz" ```


Naming convention for Packages:

In Go language, when you name a package you must always follow the following points:

- When you create a package the name of the package must be short and simple. For example strings, time, flag, etc. are standard library package.
-  The package name should be descriptive and unambiguous.
-  Always try to avoid choosing names that are commonly used or used for local relative variables.
-  The name of the package generally in the singular form. Sometimes some packages named in plural form like strings, bytes, buffers, etc. Because to avoid conflicts with the keywords.
-  Always avoid package names that already have other connotations. 

## Go Module ##

In this section, we will learn how to create the custom packages in Go.  Before creating the custom packages, we need to understand the Go Module first, since Go Modules are needed to create the custom packages.

A Go Module is nothing but a collection of Go packages. We can create the go packages using the ``go mod`` command. In addition to this, all the other third-party packages(such as source code from github) which our application uses will be present in the **go.mod** file along with the version. This **go.mod** file is created when we create a new module.

To learn more about packages, please refer the link https://golangbot.com/go-packages/ .

Enough of all theories, let's gets started with the coding part.
You can start this with any directory. In case of mine, I'm in the directory

```/Users/srikanthbhandary/Desktop/tt/MyTutorials/golang``` 

Then run the following command.

    go mod init packagetutorial 
    Output:
    go: creating new go.mod: module packagetutorial

If you open the go.mod file, and you can see the following

    module packagetutorial
    go 1.14

If you see it properly, the second line will inform you about the golang version. The first one gives information about the module name. During import, the user has to specify the package name as **package tutorial**. By convention, the module name will also include the organization name. But in the case of mine, I'm avoiding that just for the demonstration. But it's required. By default package name created in the go.mod will act as a base path for all internal and external imports.

Ex. github.com/abc/xyz

Moving forward, create a directory and name it is **circle**. Then create a file and name it is as **circle.go** inside the circle directory. After this, create a file and name it as main.go in the top-level directory. In other words, this should be inside the parent directory and not in a circle.

```
|–– golang
|   |–– circle
|       |–– circle.go
|   |–– go.mod
|   |–– main.go
```
The above diagram illustrates the information about the directory structure followed in the current code example. In your case, it could be any name given to the top-level directory.

Once the files and directories are created, edit the **circle.go** and have the following code in it. I'm lazy, but you might not be the same. Please write the code as much as possible.

```
package circle

import "math"

//CalculateArea calculates the area of a circle.
// And it recives the radius as an input parameter
func CalculateArea(radius float32) float32 {
	return math.Pi * radius * radius
}

//CalculateCircumference calculates the circumference of a circle.
// And it recives the radius as an input parameter
func CalculateCircumference(radius float32) float32 {
	return 2 * math.Pi * radius
}
```
In the above code example, you can see that I have defined two functions. And it is easily understandable by the structure of the language. If you don't know about functions, don't worry. I will teach you briefly in the upcoming sections. If you want me to explain a little bit, Ah! Yes.  You are thinking the same. Okay, I will start explaining this to you.  The first line tells about the package name. As this name says, all logical grouped components will be sitting inside the package. Remember, this is not the same as the module name.  Since area and circumference are related to a circle, I have named the package as **circle**.  


Ok, now it's time to utilize this function in the main package. If you could see this properly, here we append the module name during import. Ok, I think now you have got an idea. Here, I have imported the circle package and used the functions to calculate the Area and circumference. One thing to remember, the method or any attributes defined in the package is accessible in other packages only if it starts with the upper case. 
 

```
package main

import (
	"fmt"
	"packagetutorial/circle"
)

func main() {
	fmt.Println("Calculating area and circumference of a circle.")
	fmt.Println(circle.CalculateArea(25.0))
	fmt.Println(circle.CalculateCircumference(25.0))
}

Output:
SrikanthB-MBP golang % go run main.go
Calculating area and circumference of a circle.
1963.4955
157.07964
```

If you want to initialize any other things in package during import, you can set it that by using the special method called **init()**. And this method will not return any return values. I've slightly modified the file now. And it should be like this.

```
package circle

import (
	"fmt"
	"math"
)

func init() {
	fmt.Println("Initializing cirlce package...")
}

//CalculateArea calculates the area of a circle.
// And it recives the radius as an input parameter
func CalculateArea(radius float32) float32 {
	return math.Pi * radius * radius
}

//CalculateCircumference calculates the circumference of a circle.
// And it recives the radius as an input parameter
func CalculateCircumference(radius float32) float32 {
	return 2 * math.Pi * radius
}
```
Now check the output by running the program. As an exercise, I will leave this up to you to find the command to run main file and check the output.

I'm bored now and will come back soon with the other components of golang.

Thank you for reading cheese!





























