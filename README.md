# Sharer

![Sharer](https://raw.githubusercontent.com/Rufus31415/Sharer.NET/master/Sharer.png)

Sharer is an Arduino library that facilitates the communication between a PC and an Arduino board.
You chose the functions and variables you want to share with your desktop application and your arduino board. Functions can be easily remotly called.

Arduino versions supported: Uno, Mega 2560, Micro, Mini, Nano, Mega Adk, Bt(Bluetooth), Duemilanove, Esplora, Ethernet, Fio, Gemma, Leonardo, Lilypad, Lilypad Usb, NG, Pro, Robot Ctrl, Robot Motor, Yun, Due, Zero, 101.

## Arduino code example

``` C++
#include <Sharer.h>

// A simple function that sums an integer and a byte and return an integer
int Sum(int a, byte b) {
	return a + b;
}

// A simple function that return a^2
float Square(float a) {
	return a * a;
}

// Init Sharer and declare your function to share
void setup() {
	Sharer.init(115200); // Init Serial communication with 115200 bauds

	// Expose this function to Sharer : int Sum(int a, byte b) 
	Sharer_ShareFunction(int, Sum, int, a, byte, b);

	// Expose this function to Sharer : float Square(float a)
	Sharer_ShareFunction(float, Square, float, a);
}

// Run Sharer engine in the main Loop
void loop() {
	Sharer.run();
}
```


## [Sharer-NETStandard .NET C# code example](https://github.com/devdotnetorg/Sharer-NETStandard)

The library is based on [NET Standard 2.0](https://docs.microsoft.com/en-us/dotnet/standard/net-standard). Powered by Windows, Linux. The Net Core 3.1 test application has been successfully tested on the ARM architecture evalution board [Cubieboard A10](https://github.com/devdotnetorg/Cubieboard).

More examples [here](https://github.com/devdotnetorg/Sharer-NETStandard)
``` C#
// Connect to Arduino board
var connection = new SharerConnection("COM3", 115200);
connection.Connect();

// Scan all functions shared
connection.RefreshFunctions();

// remote call function on Arduino and wait for the result
var result = connection.Call("Sum", 10, 12);

// Display the result
Console.WriteLine("Status : " + result.Status);
Console.WriteLine("Type : " + result.Type);
Console.WriteLine("Value : " + result.Value);

// Status : OK
// Type : int
// Value : 22
```


Arduino library author: [Rufus31415](https://github.com/Rufus31415/Sharer)
