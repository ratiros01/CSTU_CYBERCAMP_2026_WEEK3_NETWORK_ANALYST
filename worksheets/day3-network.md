# Day 3 — Network Analyst (on the wire)

Read the capture with tshark (see pcap/README.md).

## A. What is in the capture?

    tshark -r pcap/capture.pcap
    tshark -r pcap/capture.pcap -Y dns -T fields -e ip.src -e dns.qry.name
    tshark -r pcap/capture.pcap -Y http.request -T fields -e ip.src -e http.request.uri

- Q1. Which IP is the normal user? Which is suspicious?
- Q2. Which file was pulled over HTTP, and why does that matter in cleartext?
- Q3. Which domain is looked up over and over? (beacon pattern)

## B. Find the flag

    tshark -r pcap/capture.pcap -Y 'frame contains "CSTU"'

- Flag 5: ______________________________

## C. Correlate with the Host side
- Q4. The attacker IP here — is it the same one in the host logs? (Y/N)
      This is the point: packet evidence corroborates log evidence.

## Problem log
Problem / What I tried / Fix / What I learned
