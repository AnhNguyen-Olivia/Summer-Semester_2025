## **Assignment 1**: 
Write a client program connecting to a server program by TCP. Client sends a string, which are inputted by a user, to server. Server will convert all letters of this string to upper-case letters and send back to Client. Client will print the data received from Server to Console.
### TCPClient.java
```java
import java.io.*;
import java.net.*;

public class TcpServer{
	public static void main(String [] args) {
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
	}
}
```
### TCPServer.java
```java
import java.io.*;
import java.net.*;

public class TcpServer{
	public static void main(String [] args) {
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
	}
}
```

**Output in Terminal:** 
```terminal
Please input a string:
beyoncé?! (gun shot, screaming)
Data from Server: BEYONCÉ?! (GUN SHOT, SCREAMING)
```

## **Assignment 2** 
Write a client program connecting to a server program by TCP. Client sends the information of a product: `(Product_Name (String)`, `Quantity (int)`, `Unit_Price (float))` which are inputted by a user from keyboard, to Server. Server will receive information of a product from Client, then print them into screen if it receives enough information of this product. This process is repeated again: User at Client can enter as many products as he wants until he enters “end” for `Product_Name`. Server also prints the information of the product until receiving “end” for product name. After that, Server print total money for all products sent by Client with formula: total money `∑ Quantity x Unit_Price`

a.      Implement Client and Server without framing (no delimiter or Length-prefix) to see why it will be bad without framing.
b.      Implement Client and Server with any delimiter which you want.
c.      Implement Client and Server with length-prefix method.

## **Assignment 3** 
Write a client program connecting to a server program by TCP. Client sends two integers (a, and b), which are inputted by a user, to server. Server will send **Least common multiple of a and b back to Client.** Client will print this number received from Server to Console.
### TCPClient.java
```java
import java.net.*;
import java.io.*;
import java.util.*;

public class TCPClient {
	public static void main(String [] args){
		try{
			Socket s = new Socket("localhost", 1234);
			
			DataInputStream Network_in = new DataInputStream(s.getInputStream());
			DataOutputStream Network_out = new DataOutputStream(s.getOutputStream());
			
			Scanner keyboard = new Scanner(System.in);
			System.out.println("Please input two integers:");
			int data1 = keyboard.nextInt();
			int data2 = keyboard.nextInt();
			
			Network_out.writeInt(data1);
			Network_out.writeInt(data2);
			
			int result = Network_in.readInt();
			System.out.println("Data from server: " + result);
			
			s.close();
		}catch(Exception e){}
	}
}
```
### TCPServer.java
```java
import java.net.*;
import java.io.*;

public class TCPSever {
	public static void main(String [] args){
		try{
				ServerSocket ss = new ServerSocket(1234);
				Socket con = ss.accept();
				
				DataInputStream in = new DataInputStream(con.getInputStream());
				DataOutputStream out = new DataOutputStream(con.getOutputStream());
				
				int num1 = in.readInt();
				int num2 = in.readInt();
				
				int result = LCM(num1, num2);
				out.writeInt(result);
				
				con.close();
			}catch(Exception e){}
	}
	
	static int euclidGCD(int num1, int num2){
		if (num2 == 0){return num1;}
		return euclidGCD(num2, num1%num2);
		}
	
	static int LCM(int num1, int num2){
		return num1*num2/euclidGCD(num1, num2);
		}
}
```

**Output in terminal:**
```terminal
Please input two integers:
98
50
Data from sever: 2450
```

## **Assignment 4** 
Write a client program connecting to a server program by TCP. Client send two integers to Server and 1 arithmetic operation (addition, subtraction, multiplication, or division) to Server. After receiving the data, Server will implement the arithmetic operation and send result back to Client. Client will print this result to Console.
### TCPClient.java
```java
import java.net.*;
import java.io.*;
import java.util.*;

public class TCPClient {
	public static void main(String [] args){
		try{
			Socket s = new Socket("localhost", 3456);
			
			DataInputStream Network_in = new DataInputStream(s.getInputStream());
			DataOutputStream Network_out = new DataOutputStream(s.getOutputStream());
			
			Scanner keyboard = new	 Scanner(System.in);
			System.out.println("Please input two integers:");
			int data1 = keyboard.nextInt();
			int data2 = keyboard.nextInt();
			keyboard.nextLine();
			
			System.out.println("Please input a arithmetic operation (+, -, *, / ):");
			String data3 = keyboard.nextLine();
			
			Network_out.writeInt(data1);
			Network_out.writeInt(data2);
			Network_out.writeUTF(data3);
			
			float result = Network_in.readFloat();
			System.out.println("Data from sever: " + result);
			
			s.close();
		}catch(Exception e){}
	}
}
```
### TCPServer.java
```java
import java.net.*;
import java.io.*;
import java.util.*;

public class TCPServer {
	public static void main(String [] args){
		try{
				ServerSocket ss = new ServerSocket(3456);
				Socket con = ss.accept();
				
				DataInputStream in = new DataInputStream(con.getInputStream());
				DataOutputStream out = new DataOutputStream(con.getOutputStream());
				
				int num1 = in.readInt();
				int num2 = in.readInt();
				
				String value = in.readUTF();
				
				float result = operation(num1, num2, value);
				out.writeFloat(result);
				
				con.close();
			}catch(Exception e){e.printStackTrace();}
	}
	
	static float operation(int num1, int num2, String value){
		switch(value) {
		case "*": return num1 * num2;
		case "+": return num1 + num2;
		case "-": return num1 - num2;
		case "/": return (float)num1/num2;
		default: return 0.0f;
		}
	}
}
```

**Output in terminal**
```terminal
Please input two integers:
6
3
Please input a arithmetic operation (+, -, *, / ):
/
Data from sever: 2.0
```

**Note**: When doing this assignment, I notice you need to change the socket number if you found the server didn't return anything. Add `e.printStackTrace()` to troubleshoot.

## **Assignment 5** 
Write a client program connecting to a server program by TCP. Client send 2 integers a, b to Server (assuming a <b). After receiving, Server send the even numbers in range [a, b]. For example, if Client send 2 and 9 to Server. Server will send one after another each number 2, 4, 6, and 8 to Client (At each time, Server only send 1 even numbers).
### TCPClient.java
```java
import java.net.*;
import java.io.*;
import java.util.*;

public class TCPClient {
	public static void main(String [] args){
		try{
			Socket s = new Socket("localhost", 1000);
			
			DataInputStream Network_in = new DataInputStream(s.getInputStream());
			DataOutputStream Network_out = new DataOutputStream(s.getOutputStream());
			
			Scanner keyboard = new	 Scanner(System.in);
			System.out.println("Please input two integers:");
			int data1 = keyboard.nextInt();
			int data2 = keyboard.nextInt();
			
			Network_out.writeInt(data1);
			Network_out.writeInt(data2);
			
			try {
				while(true){
					int result = Network_in.readInt();
					System.out.println("Data from server: " + result);
				}
			}catch(EOFException e){}
			
			s.close();
		}catch(Exception e){}
	}
}
```
### TCPServer.java
```java
import java.net.*;
import java.io.*;

public class TCPServer {

	public static void main(String [] args){
		try{
			ServerSocket ss = new ServerSocket(1000);
			Socket con = ss.accept();
				
			DataInputStream in = new DataInputStream(con.getInputStream());
			DataOutputStream out = new DataOutputStream(con.getOutputStream());
				
			int num1 = in.readInt();
			int num2 = in.readInt();
				
			for(int i = num1; i <= num2; i++){
				if(i % 2 == 0){
					out.writeInt(i);
					out.flush();
				}
			}	
			con.close();
		}catch(Exception e){e.printStackTrace();}
	}
}
```

**Output in terminal**
```terminal
Please input two integers:
5
15
Data from server: 6
Data from server: 8
Data from server: 10
Data from server: 12
Data from server: 14
```
## **Assignment 6** 
Write client and server programs to simulate the RFC862-Echo Protocol by using TCP (RFC862 - Echo Protocol [http://www.faqs.org/rfcs/rfc862.html](http://www.faqs.org/rfcs/rfc862.html))

**Assignment 7** Write client and server programs which allow a user at client side can chat with a user at server side one after another. In other words, firstly user at client side will input a string and send the string to server, server will display it on screen. Secondly, server will allow user input a string and send back to client. The process is repeated until the client or server send a string “bye”.

Note: The chat program is not parallel. We will improve it later.

(Extra) **Assignment 8** Write a client program connecting to a server program by TCP. After connection, Server sends to Client a menu:

1.      Input two integer numbers
2.      Maximum value of two numbers
3.      Minimum value of two numbers
4.      Exit

User at client side will input a number from 1 to 4 and send to Server. If user enters 1, Server will receive two integers from Client. If user enters number 2 or 3, Server will send the appropriate result. However, if user forgets to input two integers but choose 2 or 3, Server return string “please enter two integers firstly”. If user enters 4, both client and server program exit