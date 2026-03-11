**Def:** **InetAddress** represents an IP address (IPv4 or IPv6) in Java's `java.net` package. It's used in socket programming to specify network destinations more precisely than just a hostname string, like in the `Socket(InetAddress server, int port)` .

**Key Purpose**: 
- Encapsulates an IP address with optional hostname info after DNS resolution. Superclass for `Inet4Address` and `Inet6Address`.

**Common Creation Methods**:
- `InetAddress.getByName(String host)`: [[Resolves hostname to IP]] (e.g., "google.com")
- `InetAddress.getByAddress(byte[] addr)`: Creates from raw IP bytes.
- `InetAddress.getLocalHost()`: Gets this machine's IP
- `InetAddress.getLoopbackAddress()`: Returns 127.0.0.1 (local host).

**Useful Methods**:
- `getHostAddress()`: Returns string IP (e.g., "142.250.290.14")
- `getHostName()`: returns resolved hostname
- `isLoopBackAddress()`: Checks if it's a localhost
- `isReachable(int timeout)`: Pings to test connectivity.

**Example in Socket**
```java
InetAddress serverIP = InetAddress.getByName("example.com");
Socket client = new Socket(severIP, 8080); 
```
This avoids repeated DNS lookups and handles edge cases like multiple IPs per host.