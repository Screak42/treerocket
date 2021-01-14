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

*** * * * 


# Performance drop since the IPS is in-line


It's not an uncommon scenario that Network-Performance drastically drops when an IPS is put in-line.
This can have a number of reasons - very likely -  fragmented network traffic.

The IPS itself is not causing the problem, but brings a common problem to light and is amplifying it.
On first glance, the IPS seems to be responsible - when bypassed, the issue seems to be gone. Even when the IPS is removed, the fragmentation will still be present - but it's just un-noticed.
In any case, it's not a good thing to have, there will at some point be problems in the environment - with or without the IPS.
It's important to understand what fragmentation is, why it is there, and why you want to avoid it.

### What is IP fragmentation, why is it there?

In short: The MTU (Maximum Transport Unit) defines how large a packet can be. A common default value of the MTU is 1500 - The packets however are larger (possibly defined by a router) and simply don't fit into the MTU. As a result, packets need to be broken into pieces (fragments) so they fit into the MTU and then need to be re-assembled at the target.
In-Line devices like an IPS would need to do the same thing (re-assembly) and will have to wait until all packets have arrived. This does directly impact network performance in almost all cases, but is mostly un-noticed to a certain extend.
Since the IPS has to wait until all packets have arrived, no analysis can be started of this traffic until everything is complete. This will cause a delay.
But it also costs IPS performance since it requires computation - and this is a problem for us, and also very expensive (In terms of available CPU-performance vs cost of the device)  without reason.
The root cause for this can be many - it can even be an attack method as a kind of denial of service attack (Teardrop attack), but more likely it's caused by a router or a firewall elsewhere in the network. It can also be set up intentional in certain environment.
Avoiding fragmentation is often not very easy in more complex networks, and even if done intentionally not 100% where the root cause is.
It might be necessary to have various network-tabs or machines that can capture traffic in different segments to find the root cause(s) - and even then, it may not be easy to eliminate. Below are some useful links for more details, but the for us most important will be covered here on these pages.

### Why we want to avoid fragmentation and re-assembly:

- Fragmentation is an overhead - every single fragment requires an extra IP header (between 20 - 40 bytes). IPv6 adds another 8 bytes to the fragmented header.

- For what it is, it's an expensive task.
The re-assembly will consume a considerable amount of CPU. It is not highly complex, but it adds up - even for devices like routers which are designed for this task.

- There are delays to be expected (and this is what we "elevate" with the IPS) since all traffic needs to be re-assembled. This is only possible once all fragments are known or have reached their destination (or the IPS in our case). Once the first fragments are received, they will be buffered. For this the maximum possible size has to be assumed since we don't know the size yet. It is common that fragments are lost the re-assembly will be delayed even further - so the IPS will have to wait even longer.

### Wireshark and IP fragmentation, how do I see this?
Here's a few examples for this scenario.
For a quick check, an interesting display 

```
filter: ip.fragment
```
![Fragmentation](/assets/images/FR1.png)


You can download a sample of a "[Teardrop](https://wiki.wireshark.org/SampleCaptures?action=AttachFile&do=get&target=teardrop.cap)" Attack here which is pretty much exactly what IP fragmentation is.

Below is a more realistic (replicated) reflection of fragmented traffic.
We're using the filter "ip.fragment" again

![Fragmentation](/assets/images/FR2.png)
