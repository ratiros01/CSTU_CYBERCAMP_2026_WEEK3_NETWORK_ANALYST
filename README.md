# CSTU_CYBERCAMP_2026_WEEK3_NETWORK_ANALYST

Network Analyst lab — you work *on the wire*: read a packet capture with
tshark. Pairs with the Host Analyst repo (same incident, different angle).

> All IPs/domains are fake training data (RFC-5737 + .example).

## Run it

    git clone <repo-url> CSTU_CYBERCAMP_2026_WEEK3_NETWORK_ANALYST
    cd CSTU_CYBERCAMP_2026_WEEK3_NETWORK_ANALYST
    tshark -r pcap/capture.pcap                              # overview
    tshark -r pcap/capture.pcap -Y 'frame contains "CSTU"'   # Flag 5

No tshark? Open pcap/capture.pcap in Wireshark on your laptop.

## Layout
| Folder | What's inside |
|--------|----------------|
| pcap/  | capture.pcap + tshark cheat sheet |
| worksheets/ | day3-network worksheet |

Carries Flag 5. Flags 1-4 live in the Host Analyst repo.
