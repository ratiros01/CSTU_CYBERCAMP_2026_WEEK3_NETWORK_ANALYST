# tshark reference

A toolbox, not a map. These are general-purpose — which ones are useful
here is your call.

This capture has ~2,400 packets. You cannot read it all. Filtering is the
job.

## Install
- Amazon Linux:  sudo dnf install -y wireshark-cli
- Ubuntu/Kali:   sudo apt install -y tshark

## Start with statistics, not packets
Get the shape of the traffic before you read any of it.

    tshark -r capture.pcap -q -z io,phs          # what protocols are here?
    tshark -r capture.pcap -q -z endpoints,ip    # who is talking, how much?
    tshark -r capture.pcap -q -z conv,ip         # who is talking to whom?

## Reading packets

    tshark -r capture.pcap                  # every packet (long!)
    tshark -r capture.pcap -c 20            # first 20 only
    tshark -r capture.pcap -V               # full detail, every layer

## Filtering by protocol (-Y)

    tshark -r capture.pcap -Y dns
    tshark -r capture.pcap -Y http.request
    tshark -r capture.pcap -Y http.response
    tshark -r capture.pcap -Y ftp
    tshark -r capture.pcap -Y ssh

## TCP flags (useful for spotting scans)

    tshark -r capture.pcap -Y 'tcp.flags.syn==1 and tcp.flags.ack==0'
    tshark -r capture.pcap -Y 'tcp.flags.syn==1 and tcp.flags.ack==1'
    tshark -r capture.pcap -Y 'tcp.flags.reset==1'

## Pulling out fields (-T fields -e), then counting

    tshark -r capture.pcap -Y http.request -T fields -e http.user_agent
    tshark -r capture.pcap -Y dns -T fields -e dns.qry.name
    tshark -r capture.pcap -Y http.request -T fields -e ip.src -e http.request.uri

Pipe them to sort/uniq to count things:

    tshark -r capture.pcap -Y dns -T fields -e dns.qry.name | sort | uniq -c | sort -rn

## Filtering by host / port

    tshark -r capture.pcap -Y 'ip.addr==10.0.0.5'
    tshark -r capture.pcap -Y 'tcp.port==80'

## Reading a whole conversation (Follow TCP Stream)
Sometimes you want the dialogue, not individual packets:

    tshark -r capture.pcap -q -z follow,tcp,ascii,<n>

...where <n> is the stream number. Find stream numbers with:

    tshark -r capture.pcap -T fields -e tcp.stream -e ip.src -e ip.dst

## Searching the raw bytes

    tshark -r capture.pcap -Y 'frame contains "<word>"'

## Timestamps

    tshark -r capture.pcap -Y <filter> -T fields -e frame.time -e ip.src

## Tip
Wireshark display-filter syntax works here — `ip.addr==x.x.x.x`,
`http.response.code==404`, `dns.qry.name contains "..."`, and so on.
Add `-V` to any filter to see full detail of the matching packets.
