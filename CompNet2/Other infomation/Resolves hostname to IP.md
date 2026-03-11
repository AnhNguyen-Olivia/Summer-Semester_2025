`InetAddress.getByName (String host)` performs **DNS resolution** to convert a hostname like "google.com" into its actual IP address.

1. **Input**: pass a hostname string (e.g., `"google.com"`) or even a raw IP string like `"142.250.190.14"`.
2. **DNS Lookup**: Java queries the system's **DNS resolver** (usually via OS native calls): `"google.com" → DNS server → 142.250.190.14 (one of Google's IPs)`
3. **Creates InetAddress Object**: Returns `InetAddress` containing:
	- The resolved IP address
	- Cached hostname info
4. **Outcome**: 
	`Success: InetAddress addr = InetAddress.getByName("google.com"); addr.getHostAddress() → "142.250.190.14"`
	
	`Failure: UnknownHostException (host doesn't exist, no internet, DNS down)`

We use it because it is faster to ask the address one and reuse it than calling the directory every time.
```java
// String (re-resolves DNS every connect - slow)
Socket s1 = new Socket("google.com", 80);

// InetAddress (DNS cached - fast)
InetAddress addr = InetAddress.getByName("google.com");  
Socket s2 = new Socket(addr, 80);  // Uses cached IP
```
