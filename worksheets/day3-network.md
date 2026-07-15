# Day 3 — Network Analyst (on the wire)

You are a junior SOC analyst. A training server may have been touched by
someone who shouldn't have touched it. All you have is a packet capture.

Work out what happened. `pcap/README.md` has the tshark reference — which
filters you use is up to you.

    tshark -r pcap/capture.pcap

## A. Map the conversation
Before judging anything, establish what is actually here.

- Q1. Which hosts appear in this capture, and which protocols do they use?
- Q2. Build a short profile of each host that talks to the server:
      what did it ask for, what tool did it appear to use, and at what
      time of day? Record it here.

      | host | requested | tool / user-agent | time |
      |------|-----------|-------------------|------|
      |      |           |                   |      |
      |      |           |                   |      |

- Q3. Based on your table: which host behaves like a person, and which
      does not? Say why — point at the evidence, not a hunch.

## B. Question the destinations
- Q4. List every domain name that gets looked up. For each one, ask:
      does this look like somewhere a training server should be talking to?
- Q5. Does anything about the *frequency or timing* of those lookups seem
      off to you? What would that pattern mean if this were a real server?

## C. What travelled in the clear
This traffic is not encrypted. That has a consequence.

- Q6. One request pulled a file off the server. Which file, and what does
      it contain? Why is it a problem that it crossed the network like this?
- Q7. If the traffic is unencrypted, then *everything* the server sent back
      is sitting in this capture — not just the part a browser would show.
      Recover the server's full reply and read all of it.
      Did the server say anything it shouldn't have?
- Flag 5: ______________________________

## D. Correlate with the Host side
- Q8. Compare the suspicious host you identified in Part A with the logs
      from the Host Analyst lab. Same actor?
      Why does having both views matter to a SOC analyst?

## Problem log
Problem / What I tried / Fix / What I learned
