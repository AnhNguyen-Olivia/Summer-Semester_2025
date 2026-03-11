>[!SUMMARY]- Table of Contents
>- [[TCP Socket Programming-9.3.26#Review|Review]]
>- [[TCP Socket Programming-9.3.26#Client/Server Model|Client/Server Model]]
>- [[TCP Socket Programming-9.3.26#Socket|Socket]]
>- [[TCP Socket Programming-9.3.26#TCP |TCP ]]
>- [[TCP Socket Programming-9.3.26#Socket class|Socket class]]
>   - [[TCP Socket Programming-9.3.26#TCP|TCP]]
>      - [[TCP Socket Programming-9.3.26#Socket|Socket]]
>      - [[TCP Socket Programming-9.3.26#ServerSocket (Server-Side)|ServerSocket (Server-Side)]]
>- [[TCP Socket Programming-9.3.26#TCP communication|TCP communication]]
>   - [[TCP Socket Programming-9.3.26#Client Steps|Client Steps]]
>   - [[TCP Socket Programming-9.3.26#Server Steps|Server Steps]]
>- [[TCP Socket Programming-9.3.26#Examples|Examples]]
>   - [[TCP Socket Programming-9.3.26#Example 1: String to uppercase (Text Stream)|Example 1: String to uppercase (Text Stream)]]
>      - [[TCP Socket Programming-9.3.26#TCPClient.java|TCPClient.java]]
>      - [[TCP Socket Programming-9.3.26#TCPServer.java|TCPServer.java]]
>   - [[TCP Socket Programming-9.3.26#Rules|Rules]]
>   - [[TCP Socket Programming-9.3.26#Example 2: Integer Subtraction (Binary Streams)|Example 2: Integer Subtraction (Binary Streams)]]
>      - [[TCP Socket Programming-9.3.26#TCPClient.java|TCPClient.java]]
>      - [[TCP Socket Programming-9.3.26#TCPServer.java|TCPServer.java]]
>   - [[TCP Socket Programming-9.3.26#Input and Output Streams|Input and Output Streams]]
>   - [[TCP Socket Programming-9.3.26#SSL Socket|SSL Socket]]
>   - [[TCP Socket Programming-9.3.26#Example 3 "Bad" problems|Example 3 "Bad" problems]]
>      - [[TCP Socket Programming-9.3.26#Bad TCPClient.java|Bad TCPClient.java]]
>      - [[TCP Socket Programming-9.3.26#Bad TCPServer.java|Bad TCPServer.java]]
>      - [[TCP Socket Programming-9.3.26#Problem|Problem]]
>   - [[TCP Socket Programming-9.3.26#Synchronization between Client and Server|Synchronization between Client and Server]]
>   - [[TCP Socket Programming-9.3.26#Good Client with Delimiter|Good Client with Delimiter]]
>      - [[TCP Socket Programming-9.3.26#TCPClient.java|TCPClient.java]]
>      - [[TCP Socket Programming-9.3.26#TCPServer.java|TCPServer.java]]
>   - [[TCP Socket Programming-9.3.26#Good Client with Length-prefix (Recommended)|Good Client with Length-prefix (Recommended)]]
>      - [[TCP Socket Programming-9.3.26#TCPClient.java|TCPClient.java]]
>      - [[TCP Socket Programming-9.3.26#TCPServer.java|TCPServer.java]]
>   - [[TCP Socket Programming-9.3.26#Supporting many clients simultaneously|Supporting many clients simultaneously]]
>- [[TCP Socket Programming-9.3.26#Summary|Summary]]
# Review
In Java the OSI model is overkilled, thus we use TCP model
![[Pasted image 20260309191125.png]]

As the message travel down, from the top (application layer) to the bottom (physical), each layer add their headers. In application layer the PDU (protocol data units) is message, transport is segment, so on so fort. When the message sent to the destination, it will get unpacked, layer by layer. 

# Client/Server Model
In most cases, a server primary send data while a client primary receives it; but it is most rare for one program to send or receive exclusively. 

**Server** **is a host that** in theory should be **always-on**, yet in practical it can be challenged to keep a host continuously running without failures occur.  It has a **permanent IP address and often in data centers, for scaling** (to adjust the sever so it can handle more traffic)

**Client** **contact/communicate with sever**. They may be **intermittently connected** (the connection is not continuously, it can connect then stop and reconnect again). They also may have **dynamic IP addressed** (public IP and private IP). **They don't communicate directly with each other**. 

![[Pasted image 20260309195026.png]]
(P/s: there is another model, Peer-to-Peer, a host act as both a client and a server. We won't focus about it but do know in mind)
# Socket
**Socket = Address + Port number**
In more detail, **a socket is a software interface that allows a program (process) to send and receive data through a network.**

*"Let’s consider an analogy to help us understand processes and sockets. A process is analogous to a house and its socket is analogous to its door. When a process wants to send a message to another process on another host, it shoves the message out its door (socket). This sending process assumes that there is a transportation infrastructure on the other side of its door that will transport the message to the door of the destination process. Once the message arrives at the destination host, the message passes through the receiving process’s door (socket), and the receiving process then acts on the message."* 

*(page 117- Computer Networking: A Top‑Down Approach by James F. Kurose & Keith W. Ross.).*

![[Pasted image 20260309195246.png]]

# TCP 
**A connection-oriented, high-overhead but reliable protocol**. It provide **reliable, in-order byte stream** *(a sequential stream of binary data, typically processed 8 bits (one byte) at a time, used for input/output operations in computing)* **delivery as long as the connection remains establish. The connection is set up between Client and Server.** 
![[Pasted image 20260309205927.png]]
![[Pasted image 20260309210137.png]]

# Socket class
- Package java.net = `import java.net.*`
## TCP
### Socket
`java.net.Socket` = Socket handles client-side connections. 

**Constructor**: 
- `Socket(String hostname, int port)`= Connects to the specified host and port. 
- `Socket(InetAddress server, int port)` = Connects using an [[InetAddress]] object. 
- Example: `Socket("java.sun.com", 8189)`

**Method**: create some useful object from this object:
- `InputStream getInputStream()`: Returns input stream to read from server.
- `OutputStream getOutputStream()`: Returns output stream to write to server
- `close()`: Closes the socket
- `InetAddress getLocalAddress()`: Gets local address
- `int getLocalPort()`: Gets local port
- `void connect(InetSocketAddress endpoint, int timeout)`: Connects with timeout.
- `void bind(InetSocketAddress bindpoint)`: Binds to a local address
### ServerSocket (Server-Side)
Used to create servers that accept client connections.

**Constructor**: `ServerSocket(int port)`: Binds to the specified port and listens for conn.

**Method**: 
- `Socket accept()`: Blocks until a client connects, returns a Socket for that client.
- `void close()`: Closes the server socket.
# TCP communication
![[Pasted image 20260310150058.png]]

## Client Steps
1. **Create Socket**: `Socket s = new Socket("host", port);`
	Example: `Socket s = new Socket("java.sun.com", 3000);`
2. **Create Streams**: 
Input Stream (Reading):
```java
//One Line
BufferedReader in = new BufferedReader(new InputStreamReader(s.getInputStream()));

// Multiline
//Step 1: get raw byte stream from socket
InputStream rawInput = s.getInputStream();

//Step 2: Convert raw bytes to chars
InputStreamReader reader = new InputStreamReader(rawInput);

//Step 3: Add buffering for line reading
BufferedReader in = new BufferedReader(reader);
```

Output Stream (Write): 
```java
BufferedWriter out = new BufferedWritter(new OutputStreamWriter(s.getOutputStream()));
```

3. **Send/Receive Data**: 
	- Read: `String data = in.readLine()`
	- Send: `out.write("Echo: " + data + "\r\n"); out.flush()`;
4. **Close**: `s.close();`
## Server Steps
1. **Create SeverSocket**: `ServerSocket ss = new ServerSocket(port);`
	Example: `ServerSocket ss = new ServerSocket(3000)`
	**Accept Client**: `Socket con = ss.accept(); ` this block until client connects
2. **Create Streams** (from con):
Input: 
```java
BufferedReader in = new BufferedReader(new InputStreamReader(con.getInputStream()));
```
Output: 
```java
BufferedWriter out = new BufferedWriter(new OutputStreamWriter(con.getOutputStream()));
```
3. **Process data**: Read client data, process, send response
4. **Close**: `con.close();` close client socket

# Examples
Concept: `Client connects -> sends data -> Server proccesses -> responds -> close`
## Example 1: String to uppercase (Text Stream)
Write client program connecting to server program by TCP. Client sends a string, which is inputted from keyboard, to server. Server will convert all letters of this string to upper-case letters and send back to Client. Client will print the data received from Server to Console.
### TCPClient.java
```java
try{
	Socket s = new Socket("localhost", 1234);
	
	BufferedReader in = new BufferedReader(new InputStreamReader(s.getInputStream()));
	BufferedWriter out = new BufferedWriter(new OutStreamWriter(s.getOutputStream()));
	
	Scanner keyboard = new Scanner(System.in);
	System.out.println("Please input a string: ");
	String data = keyboard.nextLine();
	
	Network_out.write(data + "\r\n");
	Network_out.flush();
	String result = Network_in.readLine();
	System.out.println("Data from Server: " + result);
	
	s.close()
}catch(Exception e){e.printStackTrace();}
```
### TCPServer.java
```java
try{
ServerSocket ss = new ServerSocket(1234);
Socket con = ss.accept();

BufferedReader in = new BufferedReader(new InputStreamReader(con.getInputStream()));

BufferedWriter out = new BufferedWriter(new OutputStreamWriter(con.getOutputStream()));

String rdata = in.readLine();
System.out.println(rdata);
out.write(rdata.toUpperCase() + "\r\n");
out.flush();

con.close();

}catch (Exception e) {e.printStackTrace();}
```

## Rules
1. Server always run 1st and run 24/24
2. Client connects to server (needs IP/port)
3. Server closes `con.close` not `ss.close()`
4. Always `out.flush` after write
![[Pasted image 20260310171528.png]]
## Example 2: Integer Subtraction (Binary Streams)
Write client program connecting to server program by TCP. Client sends two integers, which are inputted from keyboard, to server. Server will calculate the result = number1 – number2 and send the result back to Client. Client will print the result received from Server to Console.

### TCPClient.java
```java
try{
Socket s = new Socket("localhost", 1234);

DataInputStream Network_in = new DataInputStream(s.getInputStream());
DataOutputStream Network_out = new DataOutputStream(s.getOutputStream());

Scanner keyboard = new Scanner(System.in);
System.out.println("Please input two integers: ");
int data1 = keyboard.nextInt();
int data2 = keyboard.nextInt();
Network_out.writeInt(data1);
Network_out.writeInt(data2);
int result = Network_in.readInt();
System.out.println("Data from server: " + result);

s.close();
}catch(Exception e){}
```

### TCPServer.java
```java
try{
ServerSocket ss = new ServerSocket(1234);
Socket con = ss.accept();

DataInputStream in = new DataInputStream(con.getInputStream());
DataOutputStream out = new DataOutputStream(con.getOutputStream());

int num1 = in.readInt();
int num2 = in.readInt();
int result = num1 - num2;
out.writeInt(result);

con.close();
}catch(Exception e){}
```

## Input and Output Streams
Java supports many I/O streams, depends on the kind of data.
- `BufferedReader/Writer` is for character-oriented data: Textual content.
- `DataInputStream/Output` is for byte-oriented data: Support primitive (int, float, char,...) java data types. Example `readInt()/writeInt()`.
- `FileInputStream/OutStream` is for file-based data like images, video,...
## SSL Socket
`javax.net.ssl` to make a connection to **SSL server** for authentication of some application protocols (POP3, SMTP,...)

Example: 
```java
SSLSocketFactory sslsocketfactory = (SSLSocketFactory)

SSLSocketFactory.getDefault();

SSLSocket pop3Socket = (SSLSocket)

sslsocketfactory.createSocket(host, port);

pop3Socket.setSoTimeout(15000);

BufferedReader in = new BufferedReader(new InputStreamReader(pop3Socket.getInputStream()));

BufferedWriter out = new BufferedWriter(new
OutputStreamWriter(pop3Socket.getOutputStream()));
```

## Example 3 "Bad" problems
Write client program connecting to server program by TCP. Client sends a string and an integer, which are inputted from keyboard, to server. Server will receive these data, store them into a string and an integer at Server side.

### Bad TCPClient.java
```java
try {
Scanner sc = new Scanner(System.in);
Socket s = new Socket("localhost", 1234);

BufferedOutputStream out = new
BufferedOutputStream(s.getOutputStream())) {

System.out.print("Enter text: ");
String text = sc.nextLine();
System.out.print("Enter number: ");
int number = Integer.parseInt(sc.nextLine());
byte[] textBytes = text.getBytes(StandardCharsets.UTF_8);
byte[] intBytes = ByteBuffer.allocate(4).putInt(number).array();

// send String
out.write(textBytes);

// send number
out.write(intBytes);
out.flush();

// notify that Client finish sending data
s.shutdownOutput(); // send EOF
System.out.println("Data sent.");

}catch (IOException e){}
```

### Bad TCPServer.java
```java
try {
ServerSocket ss = new ServerSocket(1234);
Socket con = ss.accept();

BufferedInputStream in = new BufferedInputStream(s.getInputStream());
ByteArrayOutputStream buffer = new ByteArrayOutputStream()) {
	byte[] temp = new byte[8];
	int n;
	while ((n = in.read(temp)) != -1) {
		buffer.write(temp, 0, n);
	}

	byte[] allBytes = buffer.toByteArray();
	
	if (allBytes.length < 4) {
	System.out.println("Invalid data: not enough bytes for an int.");
	return;
	}
	
byte[] textBytes = Arrays.copyOfRange(allBytes, 0, allBytes.length - 4);
byte[] intBytes = Arrays.copyOfRange(allBytes, allBytes.length - 4, allBytes.length);

String text = new String(textBytes, StandardCharsets.UTF_8);
int number = ByteBuffer.wrap(intBytes).getInt();

System.out.println("Parsed text = " + text);
System.out.println("Parsed number = " + number);}
```
### Problem
No mess boundaries in TCP (byte stream only)
- Client sends string + int as raw bytes
- Server doesn't know where strings ends, int begins
- Relies on `s.shutdownOutput()` (closes connection) => Bad design
![[Pasted image 20260311144233.png]]

## Synchronization between Client and Server
Most common student bug: **Message boundaries does not exist in TCP**. TCP is a **byte stream**, not a "messages". Server doesn't know how many bytes Client sends to. **Application must defined their own message framing**. 
- Delimiter-based: 
	- Line-delimiter (`readLine()`)
	- Self-defined
- Fixed-length records
- Length-prefix (`writeInt()` of `DataOutputStream`)
Synchronization of data transferring. 
*Q: What happens of both are waiting for data?*
A: Deadlock occurred. Solution: `flush()`

*"For example, suppose you’ve written a 300-byte request to an HTTP 1.1 server that uses*
*HTTP Keep-Alive. You generally want to wait for a response before sending any more*
*data. However, if the output stream has a 1,024-byte buffer, the stream may be waiting*
*for more data to arrive before it sends the data out of its buffer. No more data will be*
*written onto the stream until the server response arrives, but the response is never going*
*to arrive because the request hasn’t been sent yet! Figure 2-1 illustrates this catch-22.*
*The `flush()` method breaks the deadlock by forcing the buffered stream to send its data*
*even if the buffer isn’t yet full."* 

*(page 29 - Computer Networking: A Top‑Down Approach by James F. Kurose & Keith W. Ross.).*

![[Pasted image 20260311153953.png]]
*Figure 2-1. Data can get lost if you don’t flush your streams*

## Good Client with Delimiter
### TCPClient.java
```java
try {
	Scanner sc = new Scanner(System.in);
	Socket s = new Socket("localhost", 1234);
	BufferedWriter Network_out = new BufferedWriter(new
	OutputStreamWriter(s.getOutputStream()));
	System.out.print("Enter a text: ");
	String text = sc.nextLine();
	System.out.print("Enter an int: ");
	String intLine = sc.nextLine();
	out.write(textBytes + “\r\n”);
	out.write(intLine+ “\r\n”);
	out.flush(); s.close();
} catch (IOException e){}
```
### TCPServer.java
```java
will implement soon! (hw)
```

## Good Client with Length-prefix (Recommended)
Idea: 
- **Client**: before sending a string, Client will send the length of this string (4 bytes) and then send the string and number (int). 
- **Server**: read 4 bytes 1st and know the length of string. Hence, it will read the string easily, and then read the int.
### TCPClient.java
```java
Will impliment soon! (hw)
```
### TCPServer.java
```java
Will impliment soon! (hw)
```
## Supporting many clients simultaneously
With this structure, server **can not** support many TCP clients simultaneously. **Because** the current structure is sequential, server block until client answer and process that client only. The **result** is one client at a time.  For multi-client support, we use **`Threads`**, one thread per client. *(We will study this later)*
# Summary
If we use TCP for transmission, the data is delivered in order and no lost happens. Java hides all complex steps of setting up connection and data transmission between Client and Server. Client /Server program has 4 [[TCP Socket Programming-9.3.26#TCP communication|steps]] (create socket, create streams, implement function, close socket). We need to guarantee the synchronization of Client and Server.