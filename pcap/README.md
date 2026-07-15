# tshark reference

A toolbox, not a map. These are general-purpose filters — which ones are
useful here is your call.

## Install
- Amazon Linux:  sudo dnf install -y wireshark-cli
- Ubuntu/Kali:   sudo apt install -y tshark

## Reading a capture

    tshark -r capture.pcap                  # every packet, one line each
    tshark -r capture.pcap -c 10            # first 10 only
    tshark -r capture.pcap -V               # full detail, every layer

## Filtering by protocol (-Y)

    tshark -r capture.pcap -Y dns
    tshark -r capture.pcap -Y http
    tshark -r capture.pcap -Y http.request
    tshark -r capture.pcap -Y http.response

## Pulling out specific fields (-T fields -e)

    tshark -r capture.pcap -T fields -e ip.src -e ip.dst
    tshark -r capture.pcap -Y dns -T fields -e dns.qry.name
    tshark -r capture.pcap -Y http.request -T fields -e http.request.uri
    tshark -r capture.pcap -Y http -T fields -e http.user_agent

## Searching the raw bytes

    tshark -r capture.pcap -Y 'frame contains "<word>"'

## Combining
Add `-V` to any filter to see the full contents of the matching packets:

    tshark -r capture.pcap -Y <filter> -V

## Tip
Wireshark's display-filter syntax works here too — `ip.addr==x.x.x.x`,
`udp.port==53`, `http.host contains "..."`, and so on.
