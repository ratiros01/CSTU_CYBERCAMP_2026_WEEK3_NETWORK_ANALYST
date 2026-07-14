# PCAP — capture.pcap

Read it on the command line with tshark. No GUI needed (works on a
headless EC2). No tshark? Copy the file to a laptop and open Wireshark.

## Install tshark
- Amazon Linux:  sudo dnf install -y wireshark-cli
- Ubuntu/Kali:   sudo apt install -y tshark

## Beginner commands

    tshark -r capture.pcap                                   # every packet
    tshark -r capture.pcap -Y dns -T fields -e dns.qry.name  # domains looked up
    tshark -r capture.pcap -Y http.request -T fields -e ip.src -e http.request.uri
    tshark -r capture.pcap -Y 'frame contains "CSTU"'        # Flag 5

## Questions
1. Which domain looks suspicious (repeated lookups)?
2. Which file did the attacker download over plain HTTP?
3. What sensitive value is visible in the cleartext response?
4. Does the attacker IP match the one in the host logs?
