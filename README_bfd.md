<h1>BFD Command Guide</h1>
<h2>Command Summary</h2>
<h3>Configuration Mode Command</h2>

<h4>bfd monitor server</h4>
<pre>
  (no)bfd montor server A.B.C.D port <1001-65535>
</pre>

<h4>bfd monitor client</h4>
<pre>
  (no)bfd montor client A.B.C.D   Client ipv4 address (e.g. 1.2.3.4)
</pre>

<h4>bfd session</h4>
<pre>
  (no)bfd session A.B.C.D A.B.C.D
  (no)bfd session A.B.C.D <1001-65535> A.B.C.D <1001-65535>
</pre>

<h4>bfd debug</h4>
<pre>
  (no)debug bfd {event|packet|session}
</pre>

<h3>Interface Mode Command</h2>

<h4>bfd interval</h4>
<pre>
  (no) bfd interval <10-10000> min-rx <10-10000> multiplier <1-10>
</pre>

<h3>Execution Mode Command</h2>

<h4>show bfd status</h4>
<pre>
  show bfd status
</pre>

<h4>show bfd session</h4>
<pre>
  show bfd session
  show bfd session <PeerIP> <LocalIP>
  show bfd session <PeerPort> <LocalPort>
</pre>

<h4>show bfd client</h4>
<pre>
  show bfd client
</pre>


<h2>Command Detail</h2>

<h3>Configuration Mode Command</h2>

**<h4>bfd monitor server</h4>**
Set Ipv4 address and UDP port number of monitoring server.
<pre>
(no)bfd montor server [ServerIP] port [ServerUdpPort]
</pre>

<h5>Syntax Description</h5>
<pre>
ServerIP
	Monitor server’s Ipv4 Address.
ServerUdpPort
	Monitor server’s UDP Port number(1001 – 65535).
</pre>

<h5>Default</h5>
<pre>
No “bfd monitor server” are defined.
</pre>

<h5>Command Modes</h5>
<pre>
System Configuration Mode
</pre>

<h5>Example</h5>
<pre>
N1(config)#bfd monitor server 192.168.2.200 port 1005
</pre>


<h4>bfd monitor client</h4>
Set monitoring client’s Ipv4 address that will be allowed.
<pre>
(no)bfd montor client [ClientIP]
</pre>

<h5>Syntax Description</h5>
<pre>
ClientIP
	Monitor client’s Ipv4 Address.
</pre>

<h5>Default</h5>
<pre>
No “bfd monitor client” are defined.
</pre>

<h5>Command Modes</h5>
<pre>
System Configuration Mode
</pre>

<h5>Example</h5>
<pre>
N1(config)#bfd monitor client 192.168.2.200
</pre>


<h4>bfd session</h4>
“bfd session” will set session information to be learned with peer node.
<pre>
(no)bfd session [PeerIP] [LocalIP]
(no)bfd session [PeerIP] [PeerPort] [LocalIP] [LocalPort]
</pre>

<h5>Syntax Description</h5>
<pre>
PeerIP
	Peer ipv4 address.
PeerPort
	Peer UDP Port (1001 ~ 65535).
LocalIP
	Local ipv4 address.
LocalPort
	Local UDP Port (1001 ~ 65535).
</pre>

<h5>Default</h5>
<pre>
No “bfd session” are defined.
</pre>

<h5>Command Modes</h5>
<pre>
System Configuration Mode
</pre>

<h5>Example</h5>
<pre>
N1(config)# bfd session 1.1.1.12 1.1.1.11
N1(config)# no bfd session 1.1.1.12 1.1.1.11
N1(config)# bfd session 1.1.1.12 1002 1.1.1.11 1001
N1(config)# no bfd session 1.1.1.12 1002 1.1.1.11 1001
</pre>


<h4>bfd debug</h4>
debug bfd will show bfdd’s event, packet, and session related debugging message through log file.
<pre>
(no)debug bfd {event|packet|session}
</pre>

<h5>Syntax Description</h5>
<pre>
event
	event related message, ipc, socket, timer etc.
packet
	BFD protocol related message, Tx and Rx packets.
session
	sesstion DOWN/INIT/UP state related message.
</pre>

<h5>Default</h5>
<pre>
No “debug bfd” are defined.
</pre>

<h5>Command Modes</h5>
<pre>
System Configuration Mode
</pre>

<h5>Example</h5>
<pre>
N1(config)#debug bfd event
N1(config)#debug bfd packet
N1(config)#debug bfd session
</pre>


<h3>Interface Mode Command</h2>

<h4>bfd interval</h4>
Set BFD’s operational parameters per each interfaces.
<pre>
(no) bfd interval [INTERVAL] min-rx [MIN-RX] multiplier [MULTIPLIER]
</pre>

<h5>Syntax Description</h5>
<pre>
INTERVAL
	Minimum transmitting time of bfd protocol messages(milisecond)(10-10000).
MIN-RX
	Minimum receiving time of bfd protocol message (milisecond)(10-10000).
MULTIPLIER
	Multiplier number(1-10).
</pre>

<h5>Default</h5>
<pre>
No “bfd interval” are defined.
</pre>

<h5>Command Modes</h5>
<pre>
Interface Mode
</pre>

<h5>Example</h5>
<pre>
N1(config)#interface swp1
N1(interface)# bfd interval 300 min-rx 150 multiplier 3
</pre>



<h3>Execution Mode Command</h2>

<h4>show bfd status</h4>
“show bfd status” will show bfdd default parameters.
<pre>
show bfd status
</pre>

<h5>Syntax Description</h5>
<pre>
None
</pre>

<h5>Default</h5>
<pre>
No “show bfd status” are defined.
</pre>

<h5>Command Modes</h5>
<pre>
Execution Mode
</pre>

<h5>Example</h5>
<pre>
N1(exec)#show bfd status
</pre>


<h4>show bfd session</h4>
“show bfd status” will show sessions and status.
<pre>
show bfd session
show bfd session [PeerIP] [LocalIP]
show bfd session [PeerIP] [PeerPort] [LocalIP] [LocalPort]
</pre>

<h5>Syntax Description</h5>
<pre>
PeerIP
	Peer ipv4 address.
PeerPort
	Peer UDP Port (1001 ~ 65535).
LocalIP
	Local ipv4 address.
LocalPort
	Local UDP Port (1001 ~ 65535).
</pre>

<h5>Default</h5>
<pre>
No “show bfd session” are defined.
</pre>

<h5>Command Modes</h5>
<pre>
Execution Mode
</pre>

<h5>Example</h5>
N1(exec)#show bfd sessions
peer ip:port           local ip:port          status   source
...
N1(exec)#show bfd sessions 1.1.1.12 1.1.1.11
...
N1(exec)#show bfd sessions 1.1.1.12 1002 1.1.1.11 1001
...


<h4>show bfd client</h4>
“show bfd client” will show client list and each requested session information.
<pre>
show bfd client
</pre>

<h5>Syntax Description</h5>
<pre>
None
</pre>

<h5>Default</h5>
<pre>
No “show bfd client” are defined.
</pre>

<h5>Command Modes</h5>
<pre>
Execution Mode
</pre>

<h5>Example</h5>
<pre>
N1(exec)#show bfd clients
[Remote Client : 192.168.2.202]
  192.168.2.206  :3784   192.168.2.201  :3784
</pre>
