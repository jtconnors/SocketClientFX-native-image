# SocketClientFX-native-image
JavaFX UI application representing the client side of a socket connection

This application is written in Java using the Java Module System and the JavaFX API.  It is derived from the original ```SocketClientFX``` project https://github.com/jtconnors/SocketServerFX, and has been *modified to utilize GraalVM and generate a native-image version* of the ```SocketClientFX``` program. ```SocketClientFX``` represents the client side of a socket connection and can:

   - be configured to connect to either a localhost or remote socket at a configurable port
   - attempt to connect one time, or continually attempt to connect with a specified retry interval
   - send and receive text messages from a connected socket
   - retrieve sent and received messages

It is typically used in conjucntion with one of two server-side JavaFX UI applications:
```SocketServerFX``` (https://github.com/jtconnors/SocketServerFX)
or
```MultiSocketServerFX``` https://github.com/jtconnors/MultiSocketServerFX

This version of the source code is tagged ```1.0-JDK11```.  As its name suggests, it is specific to JDK 11 and can be built with the ```apache maven``` build lifecycle system.  It requires the **GraalVM Enterprise Edition SDK** as well as the **native-image** component to operate properly.  As of the creation of this project, GraalVM 20.2.0 is the latest version.

This project works on MacOS or Linux..

**Requirements:**
1. Your default JDK should point to a valid GraalVM CD JDK 11 runtime in your ```PATH```.
2. Prior to running any of the scripts in this project, either the ```JAVA_HOME``` or ```$env:JAVA_HOME``` (depending upon the platform in question) environment variable must be set to a valid GraalVM runtime.

Of note, the following maven goals can be executed:

   - ```mvn clean```
   - ```mvn dependency:copy-dependencies``` - to pull down dependent ```javafx``` and ```com.jtconnors.socket``` modules
   - ```mvn compile``` - to build the application
   - ```mvn package``` - to create the ```SocketClientFX``` modular application as a jar file
   - ```mvn exec:java``` to run the application
   - ```mvn client:build``` - to build the ```SocketClientFX``` native image.  This is a compute intensive process.  When complete, the SocketClient executable will be found in the ```target/client/${arch}/``` directory where ${arch} is either ```x86_64-darwin``` (MacOS) or ```x86_64-linux``` (Linux).
   
Furthermore, additional ```.sh```  files are provided in the ```sh/``` directoriy:
   - ```sh/run.sh``` - script file to run the application from the module path
   - ```sh/run-simplified.sh``` - alternative script file to run the application, determines main class from ```SocketClientFX``` module
   - ```sh/link.sh``` - creates a runtime image using the ```jlink``` utility


Notes:
   - These scripts have a few available command-line options.  To print out
the options, add ```-?``` or ```--help``` as an argument to any script.

See also:

- SocketServerFX: https://github.com/jtconnors/SocketServerFX
- MultiSocketServerFX: https://github.com/jtconnors/MultiSocketServerFX
- maven-com.jtconnors.socket: https://github.com/jtconnors/maven-com.jtconnors.socket
