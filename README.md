Build Location Service application with Spring Boot
Folder ShLCS_spring includes:
Location Service block, sends DIAMETER Location Request message to HSS
Web interface: Handles tasks such as entering MSISDN information; viewing log activity and data received from the DIAMETER Location Answer message
Folder test includes:
HSS block receives DIAMETER Location Request message, processes location data and returns it via DIAMETER Location Answer message
Mongo Database stores user information (Can be integrated with Open5GS's mongoDB)
LCS application on Sh interface
File ShLCS/ShLCS.java contains the Sh client block, sends User-Data Request message to the server

File ShLCS/ShServer.java contains the Sh server block, sends User-Data Answer message

GMLC built on jDiameter
Source code of jDiameter: https://github.com/RestComm/jdiameter

Specifically:

GMLC block contained in GMLC folder
Both HSS and MME blocks are contained in the Server folder
HSS in SlhServer.java
MME in SlgServer.java
File GMLC.java and config.xml contain application code to create the GMLC block and configuration for GMLC to connect to HSS and MME

Interfaces used for Diameter message exchange:

SLh: Connects to HSS (127.0.0.8)
SLg: Connects to MME (127.0.0.2)
--------------
| GMLC |
| 127.0.0.10 |
--------------
SLg / \ SLh
/ \

| MME | | HSS |
| 127.0.0.2 | | 127.0.0.8 |

Usage: Start Open5gs to create HSS and MME. Then run GMLC.

To build it yourself:

mvn install -f "pom.xml" -Dcheckstyle.skip
Throw the file example1-1.7.0-SNAPSHOT-jar-with-dependencies.jar into the path .../target/

java -classpath target/example1-1.7.0-SNAPSHOT-jar-with-dependencies.jar org.example.server.ExampleServer
Run and turn on Wireshark on lo to see the results.





# Build a Location Service application with Spring Boot.

- Folder `ShLCS_spring` including:
Web interface: Handles the task of entering MSISDN information; View activity logs and data received from the DIAMETER Location Answer message
- The `test` folder includes:

- The HSS block receives the DIAMETER Location Request message and processes the returned location data using the DIAMETER Location Answer message.

- The Mongo Database stores user information (can be combined with Open5GS's MongoDB).

# LCS application on Sh interface

The `ShLCS/ShLCS.java` file contains the Sh client block, sending the User-Data Request message to the server.

The `ShLCS/ShServer.java` file contains the Sh server block, sending the User-Data Answer message.

# GMLC built on jDiameter

JDiameter source code: https://github.com/RestComm/jdiameter

Specifically:

- The GMLC block is located in the `GMLC` folder.

- The HSS and MME blocks are both located in the `Server` folder.

- HSS is in `ShServer.java`.

- MME In `SlgServer.java`

The `GMLC.java` and `config.xml` files contain the application code to create the GMLC block and configure GMLC to connect to the HSS and MME.

The interfaces used to exchange Diameter messages are:
- SLh: Connects to HSS (127.0.0.8)
- SLg: Connects to MME (127.0.0.2)

```
            --------------
            |    GMLC    |
            | 127.0.0.10 |
            --------------
       SLg /              \ SLh
          /                \
  -------------         -------------
  |    MME    |         |    HSS    |
  | 127.0.0.2 |         | 127.0.0.8 |
  -------------         -------------

```

Instructions: Open `Open5gs` to create the HSS and MME. Then run `GMLC`.

Self-build:

```
mvn install -f "pom.xml" -Dcheckstyle.skip
```

Drag the file `example1-1.7.0-SNAPSHOT-jar-with-dependencies.jar` to the path `.../target/`
```
java -classpath target/example1-1.7.0-SNAPSHOT-jar-with-dependencies.jar org.example.server.ExampleServer
```
Run and enable Wireshark on `lo` to see the results
