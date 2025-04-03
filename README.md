# Analyzing-network-layer

# Analysis of the Situation
# 1. Protocol and Service Impacted
The network protocol impacted is UDP.

The service affected is DNS, as indicated by the error message: “udp port 53 unreachable”. Port 53 is commonly used for DNS queries.

# 2. Nature of the Issue
The ICMP error response “udp port 53 unreachable” shows that the DNS server (at IP address 203.0.113.2) was not listening on port 53.

Without a functioning DNS service, the client’s browser could not resolve the domain name www.yummyrecipesforme.com to an IP address, leading to the website being inaccessible.

# 3. Sequence of Events (as per tcpdump log)
Outgoing Request: Browser sends a DNS query via UDP to the server at 203.0.113.2.domain from the source 192.51.100.15.

# Error Response: The server responds with ICMP packets indicating that port 53 is unreachable.

Repeated Attempts: The client’s browser retries the request twice, receiving the same ICMP error.

# Follow-Up Report: DNS and ICMP Traffic Analysis

## **Incident Overview**
- **Date and Time**: (Insert specific date and time from log, e.g., 13:24:32)
- **Affected Service**: DNS (Domain Name System)
- **Impacted Protocol**: UDP
- **Error Observed**: "udp port 53 unreachable"

## **Cause of the Issue**
The error occurred because the DNS server at IP `203.0.113.2` was not listening on its designated port, `53`. This prevented DNS queries from resolving the domain `www.yummyrecipesforme.com` to an IP address. 

## **Steps Taken**
1. Attempted to access the website, which resulted in the error "destination port unreachable."
2. Used `tcpdump` to analyze traffic and confirmed:
   - UDP packets sent from the client to the DNS server (`192.51.100.15 > 203.0.113.2.domain`) failed to be delivered.
   - The DNS server responded with ICMP packets indicating that port 53 was unreachable.

## **Recommendations**
1. **Verify DNS Server Configuration**: Ensure the server is properly configured to listen on port 53.
2. **Test Network Connectivity**: Check for issues in the server's network setup that might block or misroute DNS traffic.
3. **Monitor DNS Services**: Implement monitoring tools to detect when DNS services become unavailable.
4. **Backup and Failover**: Use secondary DNS servers to handle queries in case the primary server fails.

## **Next Steps**
Report findings to the security engineers and assist in verifying server configurations to prevent further incidents.
