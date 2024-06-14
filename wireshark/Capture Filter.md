### Detailed Wireshark Capture Filters

Capture filters in Wireshark limit captured data based on specific criteria, enhancing performance and focus during data collection. These filters use a syntax derived from the Berkeley Packet Filter (BPF).

**Syntax:**
- **Basic Filters:**
  - IP Address: `host 192.168.1.1`
  - Network: `net 192.168.0.0/24`
  - Port: `port 80`
  - Protocols: `tcp`, `udp`, `icmp`

**Operators:**
- **Comparison:** `=`, `!=`, `>`, `<`
- **Logical:** `and`, `or`, `not`

**Examples:**
- Capture specific host traffic: `host 10.0.0.1`
- Capture HTTP traffic: `tcp port 80`
- Exclude specific traffic: `not port 22`

**Complex Filters:**
- Combine conditions: `(src net 192.168.1.0/24 and dst port 80) or (src port 22 and dst host 10.0.0.2)`

**Usage Tips:**
- Apply filters to reduce unnecessary data, improving capture performance.
- Use parentheses to group expressions for clarity.

**Filter Use Cases:**
- **Network Diagnostics:** Capture traffic to diagnose connectivity issues.
- **Security Analysis:** Filter traffic for suspicious activity.
- **Performance Monitoring:** Isolate traffic for performance troubleshooting.

**Examples of Wireshark Capture Filters**

1. **Capture all traffic to/from a specific host:**
   ```plaintext
   host 192.168.1.1
   ```
2. **Capture HTTP traffic (port 80):**
   ```plaintext
   tcp port 80
   ```
3. **Capture traffic within a specific subnet:**
   ```plaintext
   net 192.168.1.0/24
   ```
4. **Capture traffic from a specific IP range:**
   ```plaintext
   src net 192.168.1.0/24
   ```
5. **Capture UDP traffic:**
   ```plaintext
   udp
   ```
6. **Exclude all traffic to/from a specific host:**
   ```plaintext
   not host 10.0.0.1
   ```
7. **Capture traffic between two specific hosts:**
   ```plaintext
   host 192.168.1.1 and host 10.0.0.2
   ```
8. **Capture all traffic except ARP:**
   ```plaintext
   not arp
   ```
9. **Capture DNS traffic:**
   ```plaintext
   port 53
   ```
10. **Capture traffic from a specific MAC address:**
    ```plaintext
    ether host 00:11:22:33:44:55
    ```

For an in-depth guide, visit the [Wireshark Capture Filters page](https://wiki.wireshark.org/CaptureFilters).