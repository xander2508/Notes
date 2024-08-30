---
tags:
  - Traffic-Analysis
  - Recon
  - Network-Analysis
---

[Wireshark](https://www.wireshark.org/) is a graphical network traffic analyser. It captures and decodes frames off the wire and allows for an in-depth look into the environment. It can run many different dissectors against the traffic to characterize the protocols and applications and provide insight into what is happening.

If the GUI is not accessible see [[TShark]]

## Guide

1. Is there an authentication sequence present, see [[Wireshark#Authentication Sequence|Authentication Sequence]]

### Authentication Sequence

1. Identify the application
2. Locate username
3. Locate hash
4. Locate any additional nonces etc


## Installing Wireshark

```shell-session
sudo apt install wireshark 
```

## Wireshark Guide

![[wireshark-interface.webp]]

1. Packet List: `Orange`
    - In this window, we see a summary line of each packet that includes the fields listed below by default. We can add or remove columns to change what information is presented.
        - Number- Order the packet arrived in Wireshark
        - Time- Unix time format
        - Source- Source IP
        - Destination- Destination IP
        - Protocol- The protocol used (TCP, UDP, DNS, ETC.)
        - Information- Information about the packet. This field can vary based on the type of protocol used within. It will show, for example, what type of query It is for a DNS packet.
2. Packet Details: `Blue`
    - The Packet Details window allows us to drill down into the packet to inspect the protocols with greater detail. It will break it down into chunks that we would expect following the typical OSI Model reference. `The packet is dissected into different encapsulation layers for inspection.`
    - Keep in mind, Wireshark will show this encapsulation in reverse order with lower layer encapsulation at the top of the window and higher levels at the bottom.
3. Packet Bytes: `Green`
    - The Packet Bytes window allows us to look at the packet contents in ASCII or hex output. As we select a field from the windows above, it will be highlighted in the Packet Bytes window and show us where that bit or byte falls within the overall packet.
    - This is a great way to validate that what we see in the Details pane is accurate and the interpretation Wireshark made matches the packet output.
    - Each line in the output contains the data offset, sixteen hexadecimal bytes, and sixteen ASCII bytes. Non-printable bytes are replaced with a period in the ASCII format.

#### Capture Filters

`Capture Filters-` are entered before the capture is started. [Berkeley packet filters - IBM Documentation](https://www.ibm.com/docs/en/qsip/7.4?topic=queries-berkeley-packet-filters)
Here is a table of common and helpful capture filters with a description of each:

|       **Capture Filters**       | **Result**                                                                                                           |
| :-----------------------------: | -------------------------------------------------------------------------------------------------------------------- |
|          host x.x.x.x           | Capture only traffic pertaining to a certain host                                                                    |
|         net x.x.x.x/24          | Capture traffic to or from a specific network (using slash notation to specify the mask)                             |
|     src/dst net x.x.x.x/24      | Using src or dst net will only capture traffic sourcing from the specified network or destined to the target network |
|             port #              | will filter out all traffic except the port you specify                                                              |
|           not port #            | will capture everything except the port specified                                                                    |
|          port # and #           | AND will concatenate your specified ports                                                                            |
|          portrange x-x          | portrange will grab traffic from all ports within the range only                                                     |
|        ip / ether / tcp         | These filters will only grab traffic from specified protocol headers.                                                |
| broadcast / multicast / unicast | Grabs a specific type of traffic. one to one, one to many, or one to all.                                            |

#### Display Filters

`Display Filters-` are used while the capture is running and after the capture has stopped. Display filters are proprietary to Wireshark, which offers many different options for almost any protocol.

Here is a table of common and helpful display filters with a description of each:

|**Display Filters**|**Result**|
|:-:|---|
|ip.addr == x.x.x.x|Capture only traffic pertaining to a certain host. This is an OR statement.|
|ip.addr == x.x.x.x/24|Capture traffic pertaining to a specific network. This is an OR statement.|
|ip.src/dst == x.x.x.x|Capture traffic to or from a specific host|
|dns / tcp / ftp / arp / ip|filter traffic by a specific protocol. There are many more options.|
|tcp.port == x|filter by a specific tcp port.|
|tcp.port / udp.port != x|will capture everything except the port specified|
|and / or / not|AND will concatenate, OR will find either of two options, NOT will exclude your input option.|


## Plugins

#### Statistics Tab

The plugins here can give us detailed reports about the network traffic being utilized. It can show us everything from the top talkers in our environment to specific conversations and even breakdown by IP and protocol.

#### Analyse Tab

From the Analyse tab, we can utilize plugins that allow us to do things such as following TCP streams, filter on conversation types, prepare new packet filters and examine the expert info Wireshark generates about the traffic.

##### Following TCP Streams

Wireshark can stitch TCP packets back together to recreate the entire stream in a readable format. This ability also allows us to pull data (`images, files, etc.`) out of the capture. This works for almost any protocol that utilizes TCP as a transport mechanism.

To utilize this feature:

- right-click on a packet from the stream we wish to recreate.
- select follow → TCP
- this will open a new window with the stream stitched back together. From here, we can see the entire conversation.

Search:

```
tcp.stream eq 0
```

##### Extracting Data and Files From a Capture

Wireshark can recover many different types of data from streams. It requires you to have captured the entire conversation. Otherwise, this ability will fail to put an incomplete datagram back together.

To extract files from a stream:

- stop your capture.
- Select the File radial → Export → , then select the protocol format to extract from.
- (DICOM, HTTP, SMB, etc.)
* To export the images: Select “File → Export Objects → HTTP → `file.JPG`.

Filtering for JPEG image files:

```
http && image-jfif
```


#### Decrypt Data 

To apply the key in Wireshark:

1. go to Edit → Preferences → Protocols → TLS
2. On the TLS page, select Edit by RSA keys list → a new window will open.![[import-ws.webp]]

##### Import An RDP Key

| **Steps**                                                           |
| ------------------------------------------------------------------- |
| Click the + to add a new key                                        |
| Type in the IP address of the RDP server `10.129.43.29`             |
| Type in the port used `3389`                                        |
| Protocol filed equals `tpkt` or `blank`.                            |
| Browse to the `server.key` file and add it in the key file section. |
| Save and refresh your pcap file.                                    |

![[import-steps.webp]]

#### Fragmentation 

If our Wireshark is not reassembling packets for our inspection, we can make a quick change in our preferences for the IPv4 protocol.

![[4-frag.webp]]