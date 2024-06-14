### TShark Documentation Summary

**TShark Overview:**
TShark is the command-line version of Wireshark, designed for capturing and analyzing network traffic. It reads live data from network interfaces or from pre-captured files and can output captured data in various formats, including pcapng, to files or stdout.

**Key Options and Commands:**

- **Capture Options:**
  - `-i <interface>`: Specify the network interface to capture from.
  - `-f <capture filter>`: Apply a capture filter (in BPF syntax).
  - `-s <snaplen>`: Set the snapshot length to capture.

- **Input/Output Options:**
  - `-r <infile>`: Read packets from a capture file.
  - `-w <outfile>`: Write packets to a file.
  - `-F <format>`: Specify the output file format (e.g., pcap, pcapng).

- **Display and Filter Options:**
  - `-Y <display filter>`: Apply a display filter (Wireshark display filter syntax).
  - `-V`: Provide detailed information about each packet.
  - `-x`: Hex dump of each packet.

- **Buffer Options:**
  - `-b <option>`: Use ring buffer for capturing. Various sub-options control file size and duration.

- **Statistics and Report Options:**
  - `-q`: Run in quiet mode (less output).
  - `-z <statistics option>`: Collect and display statistics (e.g., protocols, conversations).

**Advanced Features:**
- **Name Resolution:**
  - `-n`: Disable all name resolutions.
  - `-N <type>`: Enable specific types of name resolution.

- **Packet Counting and Timing:**
  - `-c <count>`: Stop capturing after a specified number of packets.
  - `-a <autostop condition>`: Automatically stop the capture based on time, size, or file count.

**Usage Examples:**
- Capture packets on interface `eth0` and save to a file:
  ```bash
  tshark -i eth0 -w output.pcapng
  ```
- Read packets from a file and apply a display filter:
  ```bash
  tshark -r input.pcapng -Y "http.request"
  ```
- Capture with a ring buffer, creating a new file every 10 MB:
  ```bash
  tshark -i eth0 -b filesize:10240 -w output
  ```

**Documentation and Help:**
- `-h` or `--help`: Display help and exit.
- Full documentation available at [TShark man page](https://www.wireshark.org/docs/man-pages/tshark.html).

### Detailed Description

**Capture Options:**
- `-i <interface>`: Designates the network interface to be used for capturing traffic. The interface can be specified by name or index.
- `-f <capture filter>`: Defines a filter for capturing specific traffic types, using the Berkeley Packet Filter (BPF) syntax. This allows capturing only the relevant packets and reducing the data volume.
- `-s <snaplen>`: Sets the maximum size of data captured for each packet. Useful for limiting the capture size to relevant portions of packets.

**Input/Output Options:**
- `-r <infile>`: Reads packets from an existing capture file instead of capturing live traffic. This allows for the analysis of pre-captured data.
- `-w <outfile>`: Writes the captured packets to a specified file. The file format can be controlled using the `-F` option.
- `-F <format>`: Specifies the format of the output capture file. Common formats include pcap and pcapng, which are compatible with Wireshark and other analysis tools.

**Display and Filter Options:**
- `-Y <display filter>`: Applies a Wireshark display filter to the captured data. This allows for the real-time filtering of captured traffic based on criteria like protocols, IP addresses, and ports.
- `-V`: Outputs detailed information about each packet, including protocol headers and payload data.
- `-x`: Produces a hex dump of the packet data, useful for low-level analysis and debugging.

**Buffer Options:**
- `-b <option>`: Utilizes a ring buffer for capturing traffic, which can be configured to control the file size, number of files, and capture duration. This helps manage disk space and ensures continuous capturing without manual intervention.

**Statistics and Report Options:**
- `-q`: Reduces the amount of output to the console, making it easier to focus on essential information.
- `-z <statistics option>`: Collects and displays various statistics, such as protocol usage, conversation data, and endpoint information. This provides insights into network behavior and performance.

**Advanced Features:**
- **Name Resolution:**
  - `-n`: Disables all forms of name resolution, such as converting IP addresses to hostnames. This can speed up the capture process.
  - `-N <type>`: Enables specific types of name resolution, such as MAC address resolution or network address translation (NAT).

- **Packet Counting and Timing:**
  - `-c <count>`: Stops capturing after a specified number of packets have been captured. Useful for limiting the scope of a capture session.
  - `-a <autostop condition>`: Automatically stops capturing based on predefined conditions, such as capture duration, file size, or the number of files. This automates the capture process and ensures data is collected according to specific requirements.

### Usage Examples

1. **Capture on a specific interface and save to a file:**
   ```bash
   tshark -i eth0 -w output.pcapng
   ```
   This command captures traffic on the `eth0` interface and writes it to `output.pcapng`.

2. **Read packets from a file and filter HTTP requests:**
   ```bash
   tshark -r input.pcapng -Y "http.request"
   ```
   This command reads packets from `input.pcapng` and applies a display filter to show only HTTP requests.

3. **Capture using a ring buffer with a file size limit:**
   ```bash
   tshark -i eth0 -b filesize:10240 -w output
   ```
   This command captures traffic on `eth0` using a ring buffer, creating new files every 10 MB.

### Additional Information

For more detailed information, examples, and a comprehensive list of options, please refer to the full [TShark documentation](https://www.wireshark.org/docs/man-pages/tshark.html).