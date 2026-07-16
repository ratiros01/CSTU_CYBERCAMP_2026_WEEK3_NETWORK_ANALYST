# CSTU_CYBERCAMP_2026_WEEK3_NETWORK_ANALYST

Network Analyst lab — you work *on the wire*. You are handed a packet
capture from a training server and asked one question: **what happened?**

Pairs with the Host Analyst repo — same incident, different vantage point.

> All IPs/domains are fake training data (RFC-5737 + .example).

## Start

    git clone <repo-url> CSTU_CYBERCAMP_2026_WEEK3_NETWORK_ANALYST
    cd CSTU_CYBERCAMP_2026_WEEK3_NETWORK_ANALYST
    tshark -r pcap/capture.pcap | wc -l

About 2,400 packets — a few minutes of a normal office network with
something hidden in it. You can't read it all; filtering is the job. See `pcap/README.md` for the tshark reference, and
`worksheets/day3-network.md` for the investigation.

No tshark? Open `pcap/capture.pcap` in Wireshark on your laptop.

## Layout
| Folder | What's inside |
|--------|----------------|
| pcap/  | capture.pcap + tshark reference |
| worksheets/ | the Day 3 investigation |
