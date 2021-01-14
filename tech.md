---
layout: default
---
<!-- MENU BEGINN -->

<ul style="text-align: center;">
   {% for item in site.data.samplelist.docs %}
   <a href="{{ item.url }}">{{ item.title }}</a>
   |   {% endfor %}
</ul>

* * *

<!-- MENU END -->



# Out of Order Traffic (and traffic inspection problems) 


### Out of Order Traffic

Just like IP fragmenation "Out of order Traffic" is not uncommon. Often the result regarding an IPS (Intrusion Prevention System) can be, that a threat is not being detected by the IPS or performance issues.

Traffic is out of order, when packets in a specific flow are received in a different order than expected (duh...) - normally different than the sequence number dictates.
If this is the case it is difficult for an IPS device to match packets to a pattern / parameter. Most IPS's work with a kind of pattern detection or deep inspection and RegEx matching. (For example Trend Micro Tipping Point IPS's).

The packets in this flow must first be fully re-assembled to be inspected - after that they can be matched and checked against filters, RegEx etc. (This can vary from IPS to IPS but the overall principle is the same. The full flow is requited to do an analysis. You can't look at the frame of the Mona Lisa painting and tell for sure "Yep. Thats the Mona Lisa"...)

This re-assembly will cost performance on the IPS - and these devices are simply too expensive to do this - and, often it's simply not possible to re-assemble. Either, the device does not even receive the full flow, or there is a timeout set before it starts dropping the packets and moves on.
Not in all cases it will be possible to avoid "Out of order Traffic", but putting the IPS in an other place in line can often help and is a common solution. Re-directing the flow is usually more complex.
If the IPS sits outside a firwall, a loadbalancer etc. - this can happen, and may not be a problem overall, but should be considered for change if somehow possible since it has an impact on the functionality. This should be inspected very closely if it's "only" a performance impact - you might be able to life with it.

The "reroute" stats on the IPS can help to determine the percentage of packets that are out of order and require re-assembly. (Almost all IPS's should have a value like this)

Trend Micro Tipping Point devices for example have - the CLI command
debug np show all gives you a large output of useful informations.
The Table "TCP state Packet events" is very useful and has an entry "packetOoo"

![Packets Out of Order](/assets/images/WS1.png)


### Out of Order Traffic details (packet sequence)
If you'd look at this traffic capture, you would see the SEQ (sequence) number is not what we would expect to see.
It is possible that frames are forwarded earlier than expected by certain devices or the packets have traveled in a different route. 
To figure out why this is happening, it might be necessary to capture sender & recipient and compare the packet captures. It could give an answer to the root cause and if it's normal or not in this particular environment. 
If there are multiple paths between source and destination this can be normal, but from the perspective of an IPS it might need to be re-located elsewhere in the path to make sure it's functionality is not impacted. (A loadbalancer could cause this)
Packet captures that are created direclty on a firewall or loadbalancer are often out of order. This is likely ok as long as its only on this device.
If you want to look at this particular traffic for analysis though, you might not be able to work with it until it is "in order". 
In Wireshark you might be able to put things "in order" by using IP ID (ip.id) and / or SEQ (tcp.seq) columns. Also have a look below at Re-order traffic for analysis.

In a case where you ask for troubleshooting purposes for a packet capture "before and / or after an IPS" for example to isolate a particular problem, it's important to understand how these captures have been created.

If you look at packet-captures in wireshark to help and troubleshoot this, you need to make sure you understand exactly what you're looking at. Wireshark is great, but can lead to false conclusions. In some cases re-transmissions can be marked as out of order - which might not be correct. 
Also consider the environment - the capture point might be the only spot where "this" is the case - we also need to analyse what the IPS can see.
I'm stressing this fact since even the networking team might not be 100% aware how the environment is build and what else is in line.


### Wireshark and out of order traffic

The display filter reference will come in handy 
These are some useful display filters for this scenario:

```
tcp.analysis.out_of_order
tcp_dupack.pcapng
```

"A duplicate ACK is a TCP packet sent from a recipient when that recipient receives packets that are out of order. TCP uses the sequence and acknowledgment number fields within its header to reliably ensure that data is received and reassembled in the same order in which it was sent.”
*Excerpt From: Chris Sanders. “Practical Packet Analysis 3rd Edition.

Since we know this now, how can we "fix" this?

Re-order traffic for analysis
A command line tool (part of Wireshark) exists and will come in quite useful. "reordercap" It's not magic, but very good at it's job using timestamps.

```
$ reordercap -h
```

Reordercap (Wireshark) 2.6.2 (v2.6.2-0-g1b3cedbc)
Reorder timestamps of input file frames into output file.
See https://www.wireshark.org for more information.
Usage: reordercap [options] <infile> <outfile>

![Packets Out of Order example](/assets/images/WS2.png)
