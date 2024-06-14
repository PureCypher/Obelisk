Below are some Lua scripts for Wireshark that a security analyst can use to pull information such as IP addresses and device details from packet captures. These scripts leverage Wireshark's Lua API to create custom dissectors or post-dissectors.

### Script 1: Extracting IP Addresses

This script extracts IP addresses from packets and displays them in the packet details pane.

```lua
-- Extracts IP addresses from packets
local ip_addrs = {}

local ip_proto = Proto("ip_addrs", "IP Addresses Extractor")

function ip_proto.dissector(buffer, pinfo, tree)
    local ip_src_f = Field.new("ip.src")
    local ip_dst_f = Field.new("ip.dst")
    local ip_src = tostring(ip_src_f())
    local ip_dst = tostring(ip_dst_f())

    if ip_src and ip_dst then
        table.insert(ip_addrs, {src = ip_src, dst = ip_dst})
    end
end

register_postdissector(ip_proto)
```

### Script 2: Extracting Device Details

This script extracts details about devices (e.g., MAC addresses) from packets.

```lua
-- Extracts device details such as MAC addresses
local device_details = {}

local mac_proto = Proto("device_details", "Device Details Extractor")

function mac_proto.dissector(buffer, pinfo, tree)
    local eth_src_f = Field.new("eth.src")
    local eth_dst_f = Field.new("eth.dst")
    local eth_src = tostring(eth_src_f())
    local eth_dst = tostring(eth_dst_f())

    if eth_src and eth_dst then
        table.insert(device_details, {src = eth_src, dst = eth_dst})
    end
end

register_postdissector(mac_proto)
```

### Script 3: Display HTTP User-Agent

This script extracts the HTTP User-Agent string from packets, which can provide information about the device and browser used.

```lua
-- Extracts HTTP User-Agent string
local http_user_agent_proto = Proto("http_user_agent", "HTTP User-Agent Extractor")

function http_user_agent_proto.dissector(buffer, pinfo, tree)
    local http_user_agent_f = Field.new("http.user_agent")
    local user_agent = tostring(http_user_agent_f())

    if user_agent then
        tree:add(http_user_agent_proto, buffer(), "User-Agent: " .. user_agent)
    end
end

register_postdissector(http_user_agent_proto)
```

### Script 4: Extracting DNS Queries

This script extracts DNS queries from packets.

```lua
-- Extracts DNS queries from packets
local dns_queries_proto = Proto("dns_queries", "DNS Queries Extractor")

function dns_queries_proto.dissector(buffer, pinfo, tree)
    local dns_query_f = Field.new("dns.qry.name")
    local query_name = tostring(dns_query_f())

    if query_name then
        tree:add(dns_queries_proto, buffer(), "DNS Query: " .. query_name)
    end
end

register_postdissector(dns_queries_proto)
```

### Usage Instructions

1. Save the script(s) to a `.lua` file.
2. Open Wireshark and go to `Edit > Preferences > Protocols > Lua`.
3. Add the path to your Lua script file in the "Lua Script File" section.
4. Restart Wireshark to apply the changes.

These scripts will help security analysts extract relevant information from packet captures directly within Wireshark.

For more details, visit the [Wireshark Lua Documentation](https://wiki.wireshark.org/Lua).