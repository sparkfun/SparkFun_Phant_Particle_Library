# SparkFun Spark Phant Library

A Phant library for the Spark Core and Photon.

### Create a Phant Stream

Visit [data.sparkfun.com](https://data.sparkfun.com) to create a Phant stream of your own. You'll be given public and private keys, don't lose them!

If you want to set up Phant on a server of your own, visit [phant.io](http://phant.io/).

### Include & Constructor

Make sure you include "SparkFun-Spark-Phant/SparkFun-Spark-Phant.h":

	// Include the Phant library:
	#include "SparkFun-Spark-Phant/SparkFun-Spark-Phant.h":

Then create a Phant object, which requires a **server**, **public key** and **private key**:

	const char server[] = "data.sparkfun.com"; // Phant destination server
	const char publicKey[] = "DJjNowwjgxFR9ogvr45Q"; // Phant public key
	const char privateKey[] = "P4eKwGGek5tJVz9Ar84n"; // Phant private key
	Phant phant(server, publicKey, privateKey); // Create a Phant object
	
### Adding Fields/Data

Before posting, update every field in the stream using the `add([field], [value])` function. The `[field]` variable will always be a String (or const char array), `[value]` can be just about any basic data type -- `int`, `byte`, `long`, `float`, `double`, `String`, `const char`, etc.

For example:

	phant.add("myByte", 127);
	phant.add("myInt", -42);
	phant.add("myString", "Hello, world");
	phant.add("myFloat", 3.1415);

### POSTing

After you've phant.add()'ed, you can call `phant.post()` to create a Phant POST string. `phant.post()` returns a string, which you can send straight to a print function.

Most of the time, you'll want to send your `phant.post()` string straight out of a TCPClient print. For example:

	TCPClient client;
	if (client.connect(server, 80)) // Connect to the server
    {
        client.print(phant.post());
	}

After calling `phant.post()` all of the field/value parameters are erased. You'll need to make all of your phant.add() calls before calling post again.