# Day 3 — Network Analyst (on the wire)

You are a junior SOC analyst. A training server may have been touched by
someone who shouldn't have touched it. All you have is one packet capture
of about **2,400 packets** — a few minutes of a normal office network,
with something hidden in it.

You cannot read 2,400 packets. Filtering is the job.

There are **three flags** in this capture. Each one is a receipt for a
different skill — you will not find them all with one command.

    tshark -r pcap/capture.pcap | wc -l

`pcap/README.md` is your toolbox. Which filters you use is up to you.

## A. Get the shape before the detail
Never start by reading packets. Start by asking what kind of traffic exists
and who is generating it.

- Q1. What protocols are in this capture, and roughly how much of each?
- Q2. List the top talkers. Most hosts here are ordinary office
      workstations doing ordinary things. Does any host stand out by
      volume? Write down its IP.
- Q3. Is "sends the most packets" the same thing as "suspicious"? Explain
      your reasoning before you go further.

## B. Profile the hosts
- Q4. Look at the HTTP requests. What software is each host using to make
      them? Fill this in:

      | user-agent | how many requests | is this a human browsing? |
      |------------|-------------------|---------------------------|
      |            |                   |                           |
      |            |                   |                           |

- Q5. One client is not a browser. Which one, and what does that tell you
      about who — or what — is driving it?

## C. What did that host actually do?
Reconstruct its activity in order. It did several different things.

- Q6. Early on, it sends a large number of TCP packets to many different
      port numbers, very fast. What is it doing? What do the server's
      replies tell you about which ports are open?
- Q7. Finding an open port is only step one — a real analyst asks *what is
      actually running there*. Straight after the scan, this host connects
      to one of the open ports it found, reads what the service says, and
      hangs up without logging in. What is that technique called?
      Read the full conversation. Services often greet you with more than
      they should.
- Flag N1: ______________________________
- Q8. Next it makes a series of HTTP requests. Most come back with the same
      error code — what code, and what does that pattern mean it's doing?
- Q9. Those failures all return the same error page. Status codes are not
      the only thing a response carries — look at the **body** of one.
      Developers leave things in pages. Anything odd in there?
      (If it looks like nonsense text, it may not be plaintext.)
- Flag N2: ______________________________
- Q10. Among all those failures, at least one request **succeeded**. Which
       file did it get? Why does that file matter?

## D. What travelled in the clear
This traffic is not encrypted. That has a consequence.

- Q11. The successful download crossed the network readable. What sensitive
       value is now exposed? Why is HTTP the real problem here, not the file?
- Q12. If nothing is encrypted, then *everything* the server sent back is in
       this capture — not just the part a browser would display. Recover the
       server's full reply to that request and read all of it.
       Did the server say anything it shouldn't have?
- Flag N3: ______________________________

## E. Outbound traffic — the part everyone forgets
So far you looked at traffic coming *in*. Now look at what the server sends
*out*.

- Q13. List every domain looked up in this capture, with a count. Most are
       normal company services. One is not.
- Q14. Careful: the odd-looking one is not the most frequent. Rank by
       "how many times" and you will pick the wrong host. For each domain
       ask instead:
       - who is asking for it? (a workstation, or the server itself?)
       - how regular is the timing?
       What did you find, and why is regular timing suspicious?
- Q15. What would you call this behaviour, and what does it suggest about
       the state of the server?

## F. Correlate with the Host side
- Q16. Compare the suspicious host from Part B with the logs from the Host
       Analyst lab. Same actor?
- Q17. You found the scan and the download here. The Host lab found the
       failed logins. Why does a SOC need both views?

## Problem log
Problem / What I tried / Fix / What I learned
