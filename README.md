<h1>
TWAMP Command

<h2> 1.	Configuration Mode Command

<h3>1.1. 	**twamp light** command
<h5> twamp light

<pre><h6> Start the TWAMP light server. By default, the server receive and response twamp-test packets from any client.

<pre><h6>twamp light
no twamp light

<h5> Syntax Description
<pre><h6> None

<h5> Default
<pre><h6> Default is “no twamp light”.

<h5> Command Modes
<pre><h6> System Configuration Mode

<h5> Example
<pre><h6>N1(config)# twamp light
N1(config)# no twamp light

<h3>1.1.1	**reflector-port** command
<h5>reflector-port
<pre><h6>reflector udp port that receive and response twamp-test packets from any client.
<pre><h6>reflector-port <100-100000>
no reflector-port

<h5>Syntax Description
<pre><h6>None

<h5>Default
<pre><h6>Default is 862.

<h5>Command Modes
<pre><h6>Twamp light Mode

<h5>Example
<pre><h6>N1(config)# twamp light
N1(twamp-light)# reflector-port 1000
N1(twamp-light)# no reflector-port


<h3>1.2. 	**twamp server** command
<h5>twamp server
<pre><h6>Start the TWAMP server. By default, the server accepts any connection request from any client.

twamp server
no twamp server

<h5>Syntax Description
None

<h5>Default
Default is “no twamp server”.

<h5>Command Modes
System Configuration Mode

<h5>Example
N1(config)# twamp server
N1(config)# no twamp server


2.2.1	< control-packet-dscp > command
control-packet-dscp
Specify value as the DSCP byte in the IP header of control packets sent from the server.

(no) control-packet-dscp <0-255>

Syntax Description
<0-255>
	DSCP value

Default
Default value is ”zero”.

Command Modes
Twamp server Mode

Example
N1(config)# twamp server
N1(twamp-server)# control-packet-dscp 12
N1(twamp-server)# no control-packet-dscp

[Note] DSCP Rule(control and test packet)
twamp(dec)	bin	TCP/IP Stack(dec)	bin
0	00000000	0	00000000
1	00000001	0	00000000
2	00000010	0	00000000
3	00000011	0	00000000
4	00000100	4	00000100
5	00000101	4	00000100
6	00000110	4	00000100
7	00000111	4	00000100
8	00001000	8	00001000
9	00001001	8	00001000
10	00001010	8	00001000
11	00001011	8	00001000
12	00001100	12	00001100
13	00001101	12	00001100
14	00001110	12	00001100
15	00001111	12	00001100
16	00010000	16	00010000
17	00010001	16	00010000
18	00010010	16	00010000
19	00010011	16	00010000
20	00010100	20	00010100
21	00010101	20	00010100
22	00010110	20	00010100
23	00010111	20	00010100
24	00011000	24	00011000
25	00011001	24	00011000
26	00011010	24	00011000
27	00011011	24	00011000
…	…	…	…
248	11111000	248	11111000
249	11111001	248	11111000
250	11111010	248	11111000
251	11111011	248	11111000
252	11111100	252	11111100
253	11111101	252	11111100
254	11111110	252	11111100
255	11111111	252	11111100


2.2.2	< maximum-connections > command
Server maximum-connections
Specify value as the maximum number of control sessions for each TWAMP server.

(no) maximum-connections <1-100>

Syntax Description
<1-100>
Maximum connections value default 10

Default
Default value is “10”.

Command Modes
twamp server mode

Example
N1(config)# twamp server
N1(twamp-server)# maximum-connections 11
N1(twamp-server)# no maximum-connections


2.2.3	< maximum-sessions-per-connection > command
maximum-sessions-per-connection
Limit the number of maximum number of test sessions for each control session.

(no) maximum-sessions-per-connection <1-100>

Syntax Description
<1-100>
	the number of maximum number of test sessions for each control session

Default
Default value is ”10”.

Command Modes
twamp server Mode

Example
N1(config)# twamp server
N1(twamp-server)# maximum-sessions-per-connection 11
N1(twamp-server)# no maximum-sessions-per-connection


2.2.4	< mode > command
server mode
enable security mode.

(no) twamp server mode {unauthenticated | authenticated | encrypted | mixed}

Syntax Description
unauthenticated
	unauthenticated mode
authenticated
	authenticated mode
encrypted
	encrypted mode
mixed
	control packets are encrypted and test packets are unauthenticated.

Default
Default value is unauthenticated mode.

Command Modes
System Configuration Mode

Example
N1(config)# twamp server
N2(twamp-server)# mode unauthenticated authenticated encrypted mixed
N2(twamp-server)# no mode unauthenticated authenticated encrypted mixed


2.2.5	< server-tcp-port> command
port
Specify number as the TCP port used for control sessions.

(no) server-tcp-port <100-100000>

Syntax Description
value
	number as the TCP port

Default
Default number is “862”.

Command Modes
Twamp server Mode

Example
N1(config)# 
N1(twamp-server)# server-tcp-port 862
N1(twamp-server)# no server-tcp-port


2.2.6	<max-count> command
Max-count
This parameter limits the maximum Count value..

(no) max-count <1024-32768>

Syntax Description
<1024-32768>
	Count value for deriving key. default 32768

Default
Default number is “32768”.

Command Modes
Twamp server Mode

Example
N1(config)# 
N1(twamp-server)# max-count 1024
N1(twamp-server)# no max-count


2.2.7	< count > command
count
Parameter used in deriving a key from a shared secret as described in Section 3.1 of RFC 4656, and are communicated to the Control-Client as part of the Server Greeting message.

(no) count <1024-32768>

Syntax Description
<1024-32768>
	Count value for deriving key. default 1024

Default
Default number is “1024”.

Command Modes
Twamp server Mode

Example
N1(config)# 
N1(twamp-server)# count 1024
N1(twamp-server)# no count


2.2.8	< base-test-port > command
Max-count
This parameter is the value of dynamic allocated UDP port of test packet.

(no) base-test-port <1024-65535>

Syntax Description
<1024-65535>
	UDP port number. default 20000

Default
Default number is “20000”.

Command Modes
Twamp server Mode

Example
N1(config)# 
N1(twamp-server)# base-test-port 20001
N1(twamp-server)# no base-test-port


2.2.9	< serv-ref-wait > command
servwait
Set the timeout value for control-session inactivity in seconds. Indicates that the TWAMP-Control connection to the Control-Client is in SERVWAIT according to RFC 5357 (Section 3.1): [a] Server MAY discontinue any established control connection when no packet associated with that connection has been received within SERVWAIT seconds.

(no) servwait <1-604800>

Syntax Description
value
	timeout value for control-session

Default
Default number is “900”.

Command Modes
System Configuration Mode

Example
N1(config)# twamp server
N1(twamp-server)# serv-ref-wait 100
N1(twamp-server)# no serv-ref-wait 100


2.2.10	< key-chain > command
Key-chainserver user user-string password password-string
Enter key-chain mode.

key-chain
no key-chain

Syntax Description
None

Default
None

Command Modes
twamp server mode

Example
N1(twamp-server)# key-chain
N1(twamp-server)# no key-chain


2.2.11	< key-id > command
key-id
Set key-id and secure-key

key-id WORD secret-key WORD
no key-id WORD

Syntax Description
Key-id
	string for key-name
secure-key
	string for passprase

Default
None

Command Modes
twamp server key-chain mode

Example
N1(twamp-server-key-chain)# key-id KEY01 secure-id SECURE01
N1(twamp-server-key-chain)# no key-id


2.3. 	<twamp client> command
twamp client
Enter the TWAMP client configuration mode. 

(no) twamp client

Syntax Description
None

Default
Default is “no twamp client”.

Command Modes
System Configuration Mode

Example
N1(config)# twamp client
N1(config)# no twamp client


2.3.1	< mode-preference > command
mode-preference
Enter “twamp client mode-preference” mode. 

(no) mode-preference

Syntax Description
None

Default
None

Command Modes
twamp client mode

Example
N1(twamp-client)# mode-preference
N1(twamp-client)# no mode-preference


2.3.1.1	< priority > command
priority
Specify value as the DSCP byte in the IP header of control packets sent from the server.

(no) priority <0-3> mode (unauthenticated|authenticated|encrypted|mixed)

Syntax Description
<0-3>
	Mode priority
unauthenticated|authenticated|encrypted|mixed
	Supported TWAMP Mode.

Default
unauthenticated.

Command Modes
Twamp server mode-preference mode

Example
N1(config)# twamp server
N1(twamp-server)# mode-preference
N1(twamp-server-mode-preference)# priority 0 mode unauthenticated
N1(twamp-server-mode-preference)# priority 1 mode authenticated
N1(twamp-server-mode-preference)# priority 2 mode encrypted
N1(twamp-server-mode-preference)# priority 3 mode mixed
N1(twamp-server-mode-preference)# no priority 0
N1(twamp-server-mode-preference)# no priority 1
N1(twamp-server-mode-preference)# no priority 2
N1(twamp-server-mode-preference)# no priority 3

2.3.2	< key-chain > command
key-chain
Enter “twamp client key-chain” mode. 

(no) key-chain

Syntax Description
None

Default
None

Command Modes
twamp client mode

Example
N1(twamp-client)# key-chain
N1(twamp-client)# no key-chain


2.3.2.1	< key-id > command
key-id
Set key-id and secure-key

(no) key-id WORD secret-key WORD

Syntax Description
Key-id
	string for key-name
secure-key
	string for passprase

Default
None

Command Modes
twamp server key-chain mode

Example
N1(twamp-server-key-chain)# key-id KEY01 secure-id SECURE01
N1(twamp-server-key-chain)# no key-id KEY01


2.3.3	< control-connection > command
control-connection
Enter “twamp client control-connection” mode. 

(no) control-connection WORD

Syntax Description
WORD
	String for Control-connection name

Default
None

Command Modes
twamp client mode

Example
N1(twamp-client)# control-connection CONN-01
N1(twamp-client)# no control-connection CONN-01


2.3.3.1	< client-ip > command
client-ip
Set client ip address for twamp control.

(no) client-ip A.B.C.D

Syntax Description
A.B.C.D
	Ipv4 address format

Default
None

Command Modes
twamp server control-connection mode

Example
N1(twamp-server-control-connection)# client-ip 1.1.1.1
N1(twamp-server-control-connection)# no client-ip


2.3.3.2	< server-ip > command
server-ip
Set server ip address for twamp control.

(no) server-ip A.B.C.D

Syntax Description
A.B.C.D
	Ipv4 address format

Default
None

Command Modes
twamp server control-connection mode

Example
N1(twamp-server-control-connection)# server-ip 1.1.1.1
N1(twamp-server-control-connection)# no server-ip

2.3.3.3	< server-tcp-port > command
server-tcp-port
Set server control tcp port for twamp control.

server-tcp-port <100-65535>
no server-tcp-port

Syntax Description
<100-65535>
	server tcp port number

Default
Default tcp port number is 862

Command Modes
twamp server control-connection mode

Example
N1(twamp-server-control-connection)# server-tcp-port 863
N1(twamp-server-control-connection)# no server-tcp-port


2.3.3.4	< control-packet-dscp > command
control-packet-dscp
Set dscp value for control connection. The DSCP value to be placed in the IP header of TWAMP-Control (TCP) packets generated by this Control-Client.

control-packet-dscp <0-255>
no control-packet-dscp

Syntax Description
<0-255>
	dscp value

Default
Default tcp port number is 0

Command Modes
twamp server control-connection mode

Example
N1(twamp-server-control-connection)# control-packet-dscp 5
N1(twamp-server-control-connection)# no control-packet-dscp


2.3.3.5	< key-id > command
control-packet-dscp
Set key-id string for control connection. The KeyID value that is selected for this TWAMP-Control connection.

key-id WORD
no key-id

Syntax Description
WORD
	String value for key-id

Default
None

Command Modes
twamp server control-connection mode

Example
N1(twamp-server-control-connection)# key-id KEY-01
N1(twamp-server-control-connection)# no key-id


2.3.3.6	< max-count > command
max-count
Set max-count for count. This parameter limits the maximum Count value. If an attacking system sets the maximum value in Count (2**32), then the system under attack would stall for a significant period of time while it attempts to generate keys.

(no) max-count <1024-32768>

Syntax Description
<1024-32768>
	Maximum value for count.

Default
Default number is 32768

Command Modes
twamp server control-connection mode

Example
N1(twamp-server-control-connection)# max-count 2048
N1(twamp-server-control-connection)# no max-count


2.3.3.7	< session-request > command
session-request
Enter “twamp client control-connection session-request” mode. Information associated with the Control-Client for this test session

session-request WORD
no session-request WORD

Syntax Description
WORD
	String for session-request name

Default
None

Command Modes
twamp client control-connection mode

Example
N1(twamp-client-control-connection)# session-request SESS-REQ-01
N1(twamp-client-control-connection)# no session-request SESS-REQ-01


2.3.3.7.1	< sender-ip > command
sender-ip
Set sender ip address for twamp test. The IP address of the Session-Sender device, which is to be placed in the source IP address field of the IP header in TWAMP-Test (UDP) packets belonging to this test session. This value will be used to populate the sender address field of the Request-TW-Session message. If not configured, the device SHALL choose its own source IP address.

sender-ip A.B.C.D
no sender-ip

Syntax Description
A.B.C.D
	Ipv4 address format

Default
None

Command Modes
twamp client control-connection session-request mode

Example
N1(twamp-client-session-request)# sender-ip 1.1.1.1
N1(twamp-client-session-request)# no sender-ip

2.3.3.7.2	< sender-udp-port > command
sender-udp-port
Set sender udp port for twamp test. The UDP port number that is to be used by the Session-Sender for this TWAMP-Test session. The number is restricted to the dynamic port range. A value of zero indicates that the Control-Client SHALL auto-allocate a UDP port number for this TWAMP-Test session. The configured (or auto-allocated) value is advertized in the Sender Port field of the Request-TW-session message (see also Section 3.5 of RFC 5357. Note that in the scenario where a device auto-allocates a UDP port number for a session, and the repeat parameter for that session indicates that it should be repeated, the device is free to auto-allocate a different UDP port number when it negotiates the next (repeated) iteration of this session.

sender-udp-port <100-65535>
no sender-udp-port

Syntax Description
<100-65535>
	Sender udp port.

Default
None

Command Modes
twamp client control-connection session-request mode

Example
N1(twamp-client-session-request)# sender-udp-port 10000
N1(twamp-client-session-request)# no sender-udp-port

2.3.3.7.3	< reflector-ip > command
reflector-ip
Set reflector ipv4 address for twamp test. The IP address belonging to the remote Session-Reflector device to which the TWAMP-Test session will be initiated. This value will be used to populate the receiver address field of the Request-TW-Session message

reflector-ip A.B.C.D
no reflector-ip

Syntax Description
A.B.C.D
	Reflector ipv4 address

Default
None

Command Modes
twamp client control-connection session-request mode

Example
N1(twamp-client-session-request)# reflector-ip 1.1.1.2
N1(twamp-client-session-request)# no reflector-ip

2.3.3.7.4	< reflector-udp-port > command
reflector-udp-port
Set reflector udp port for twamp test. This parameter defines the UDP port number that will be used by the Session-Reflector for this TWAMP-Test session. The number is restricted to the dynamic port range and is to be placed in the Receiver Port field of the Request-TW-Session message. If this value is not set, the device SHALL use the same port number as defined in the server-tcp-port parameter of this test-session-request’s parent twamp/client/ctrl-connection.

reflector-udp-port <100-65535>
no reflector-udp-port

Syntax Description
<100-65535>
	Reflector udp port

Default
None

Command Modes
Twamp client/control-connection/session-request mode

Example
N1(twamp-client-session-request)# reflector-udp-port 10000
N1(twamp-client-session-request)# no reflector-udp-port

2.3.3.7.5	< timeout > command
timeout
Set timeout for twamp test.  The length of time (in seconds) that the Session-Reflector should continue to respond to packets belonging to this TWAMP-Test session after a Stop-Sessions TWAMP-Control message has been received (RFC 5357, Section 3.8). This value will be placed in the Timeout field of the Request-TW-Session message.

timeout <0-100>
no timeout

Syntax Description
<0-100>
	Timeout seconds

Default
Default timeout is 2 seconds

Command Modes
Twamp client/control-connection/session-request mode

Example
N1(twamp-client-session-request)# timeout 10
N1(twamp-client-session-request)# no timeout

2.3.3.7.6	< test-packet-dscp > command
test-packet-dscp
Set dscp value for twamp test. The DSCP value to be placed in the IP header of TWAMP-Test packets generated by the Session-Sender, and in the UDP header of the TWAMP-Test response packets generated by the Session-Reflector for this test session. This value will be placed in the Type-P Descriptor field of the Request-TW-Session message (RFC 5357).

test-packet-dscp <0-255>
no test-packet-dscp

Syntax Description
<0-255>
	Test packet’s dscp value.

Default
Default test packet’s dscp is 0

Command Modes
Twamp client/control-connection/session-request mode

Example
N1(twamp-client-session-request)# test-packet-dscp 10
N1(twamp-client-session-request)# no test-packet-dscp

2.3.3.7.7	< repeat > command
repeat
Set repeat value for twamp test. This value determines if the TWAMP-Test session must be repeated. When a test session has completed, the repeat parameter is checked. The value of 0 indicates that the session MUST NOT be repeated. If the value is 1 through 4,294,967,294 then the test session SHALL be repeated using the information in repeat-interval parameter, and the parent TWAMP-Control connection for this test session is restarted to negotiate a new instance of this TWAMP-Test session. The implementation MUST decrement the value of repeat after determining a repeated session is expected. The value of 4,294,967,295 indicates that the test session SHALL be repeated *forever* using the information in repeat-interval parameter, and SHALL NOT decrement the value.

repeat <0-4294967294>
no repeat

Syntax Description
<0-4294967294>
	Repeat number

Default
Default repeat valule is 0

Command Modes
Twamp client/control-connection/session-request mode

Example
N1(twamp-client-session-request)# repeat 10
N1(twamp-client-session-request)# no repeat

2.3.3.7.8	< repeat-interval > command
repeat-interval
Set repeat-interval value for twamp test. This parameter determines the timing of repeated test sessions when repeat is more than 0. When the value of repeat-interval is 0, the negotiation of a new test session SHALL begin immediately after the previous test session completes. Otherwise, the Control-Client will wait for the number of minutes specified in the repeat-interval parameter before negotiating the new instance of this TWAMP-Test session.

repeat-interval <0-4294967294>
no repeat-interval

Syntax Description
<0-4294967294>
	Repeat-interval time (minutes)

Default
Default repeat-interval valule is 0

Command Modes
Twamp client/control-connection/session-request mode

Example
N1(twamp-client-session-request)# repeat-interval 10
N1(twamp-client-session-request)# no repeat-interval


2.3.4	< monitor > command
monitor
Enter “twamp client monitor” mode. 

(no) monitor

Syntax Description
None

Default
None

Command Modes
twamp client mode

Example
N1(twamp-client)# monitor
N1(twamp-client)# no monitor


2.3.4.1	< max-connection > command
max-connection
Set the number of max clients to be connected

(no) max-connection <1-10>

Syntax Description
<1-10>
	Number of max clients

Default
5

Command Modes
twamp client monitor mode

Example
N1(twamp-client-monitor)# max-connection 6
N1(twamp-server-control-connection)# no max-connection

2.3.4.2	< listen-tcp-port > command
listen-tcp-port
Set tcp listen port number for monitor clients to be connect

(no) listen-tcp-port <100-65535>

Syntax Description
<100-65535>
	Tcp-port number

Default
22222

Command Modes
twamp client monitor mode

Example
N1(twamp-client-monitor)# listen-tcp-port 22222
N1(twamp-server-control-connection)# no listen-tcp-port

2.3.4.3	< client-ip > command
client-ip
Set monitor client ip to be allowed

(no) client-ip A.B.C.D

Syntax Description
A.B.C.D
	Ipv4 address

Default
None

Command Modes
twamp client monitor mode

Example
N1(twamp-client-monitor)# client-ip 1.2.3.4
N1(twamp-server-control-connection)# no client-ip


2.4. 	<twamp sender> command
twamp sender
Enter the TWAMP sender configuration mode. 

(no) twamp sender

Syntax Description
None

Default
Default is “no twamp sender”.

Command Modes
System Configuration Mode

Example
N1(config)# twamp sender
N1(config)# no twamp sender


2.4.1	< test-session > command
test-session
Enter “twamp sender/test-session” mode. 

(no) test-session WORD

Syntax Description
WORD
	String value for test-session

Default
None

Command Modes
twamp sender mode

Example
N1(twamp-sender)# test-session TEST-01
N1(twamp-sender)# no test-session TEST-01

2.4.1.1	< control-connection-name > command
control-connection-name
Specify control-connection-name. The name of the parent TWAMP-Control connection that is responsible for negotiating this TWAMP-Test session.

(no) control-connection-name WORD

Syntax Description
WORD
	String value for control-connection.

Default
None

Command Modes
Twamp sender test-session mode

Example
N1(twamp-sender- session-request)# control-connection-name CONN-01
N1(twamp-sender- session-request)# no control-connection-name CONN-01


2.4.1.2	< number-of-packet > command
number-of-packet
Specify number of packet. The overall number of TWAMP-Test (UDP) packets to be transmitted by the Session-Sender for this test session.

number-of-packet <1-4294967295>

Syntax Description
<1-4294967295>
	Number of packet

Default
Default is 1

Command Modes
Twamp sender test-session mode

Example
N1(twamp-sender- session-request)# number-of-packet 10
N1(twamp-sender- session-request)# no number-of-packet


2.4.1.3	< interval > command
interval
Interval time between each test packets.

(no) interval <1-4294967295> sec | msec

Syntax Description
<1-4294967295>
	Interval time between test packets

Default
Default is 1 secconds

Command Modes
Twamp sender test-session mode

Example
N1(twamp-sender- session-request)# interval 1 sec
N1(twamp-sender- session-request)# no interval

3.	Exec Command
3.1. 	< show twamp light > command
3.1.1	<show twamp light status> command
show service twamp light status
Show twamp light parameters.

show twamp light status

Syntax Description
None

Default
None is defined.

Command Modes
System Execution Mode

Example
N1(exec)# show twamp light status

3.2. 	< show twamp server > command
3.2.1	<show twamp server status> command
show service twamp server status
Show twamp parameters.

show twamp server status
show twamp server

Syntax Description
None

Default
None

Command Modes
System Execution Mode

Example
N2(exec)#show twamp server status 
  twamp server enable
  dscp value : 12
  maximum connections : 10
  maximum sessions per connection : 10
  auth-mode : Unauthenticated Authenticated Encrypted Mixed
  control tcp port : 862
  control key max-count : 32768
  control key count : 1024
  test udp base port : 20000
  control inactivity timeout : 130 seconds
  test inactivity timeout : 65 seconds


3.2.2	< show twamp server sessions > command
show twamp server session
Show all sessions of twamp connection

show twamp server session

Syntax Description
None

Default
None

Command Modes
System execution mode

Example
N1(exec)#show twamp server sessions
[client ip/port 192.168.137.253/45012 server ip/port 192.168.137.187/862]
  status : Testing
  mode : Authenticated
  time remaining : active
  key-id : key01
  number of test session : 1
    SID : b9afff5cabeed8253c762711de03e019
      time remaining : refwait 62 seconds
      mode : Authenticated
      sender-ip/port : 1.1.1.1/20001
      receiver-ip/port : 1.1.1.2/30001


3.2.3	<show twamp server session detail> command
show twamp server sessions
Show all sessions’s detail information of twamp connections

show twamp server session detail

Syntax Description
None

Default
None

Command Modes
System execution mode

Example
N1(exec)#show twamp server sessions detail
[client ip/port 192.168.137.253/47838 server ip/port 192.168.137.187/862]
  status : Testing
  mode : Authenticated
  time remaining : active
  key-id : key01
  challenge : a2d20a4b031e8b28d067ba92a969aee4
  salt : 604f2c8d1fab53ac39944705bc742865
  count : 1024
  aes-session-key : 5c7c0563e419c71a8b9dc472fae5b0df
  hmac-sha1-session-key : 85408512331543ef7080151f02c038d54e6541593dc3c818442238596f5fee39
  encryption-key : 0951737018040eff99230a9955715077
  client-iv : 3cc11d637b781072e9824311a8da4782
  server-iv : d586bdc013b21bed46a3f34e9d941076
  number of test session : 1
    SID : 73344c8aa20a9a2ef213cb5ad4489a86
      time remaining : refwait 9 seconds
      mode : Authenticated
      sender-ip/port : 1.1.1.1/20001
      receiver-ip/port : 1.1.1.2/30001
      test-aes-session-key : e8df902b6cb1493e8741ad61a738aca2
      test-hmac-sha1-session-key : fa534b41f3fe6003208df8388c8d2fdfbb05de16aaaa276e767ce571be8d2eca


3.3. 	< show twamp client > command
3.3.1	<show twamp client status> command
show service twamp server status
Show twamp client parameters.

show twamp client
show twamp client status

Syntax Description
None

Default
None

Command Modes
System Execution Mode

Example
N1(exec)#show twamp client
N1(exec)#show twamp client
twamp client
  monitor-client
    client-ip/port : 192.168.122.101/39984
  mode-preference-chain
    0 authenticated
    1 encrypted
    2 mixed
  key-chain
    key01 secret01
  control-connection CONN-N2
    server IP : 192.168.122.102
    key-id : key01
    session request name : SESS-01
      reflector IP : 1.1.1.12


3.3.2	< show twamp client session > command
show twamp client session
Show all information of twamp client sessions

show twamp client session

Syntax Description
None

Default
None

Command Modes
System execution mode

Example
N1(exec)#show twamp client session 
[client ip/port 192.168.122.101/48470 server ip/port 192.168.122.102/862]
  name : CONN-N2
  status : active
  mode : Authenticated
  key-id : key01
  number of test session : 1
    SID : 17e43a200d0f4ea8668f43a2e43344a1
      mode : Authenticated
      sender-ip/port : 1.1.1.11/20000
      receiver-ip/port : 1.1.1.12/20000

3.3.3	<show twamp client session WORD> command
show twamp client session WORD
Show detail informations of specific twamp session.

show twamp client session WORD

Syntax Description
None

Default
None

Command Modes
System execution mode

Example
N1(exec)#show twamp client session CONN-N2
[client ip/port 192.168.122.101/48470 server ip/port 192.168.122.102/862]
  name : CONN-N2
  status : active
  mode : Authenticated
  key-id : key01
  challenge : 7055887deab2d465a102259a3bdf5885
  salt : 0756f25976e26c9b903662b254db6ac3
  count : 262144
  aes-session-key : 0c624c2b4c70d7c1ee58cc3bcdd17c62
  hmac-sha1-session-key : 9210a6cd81c4e8ec75371e76f370feba532dfefc3d03dbe3ee29e1396097d74a
  encryption-key : e1ea0c679a9a8faa05f90b0d42e71b8a
  client-iv : b1fa25cf69f1b325c10721829399c748
  server-iv : bb69db7e3760b6062e9aaf8b738caf02
  number of test session : 1
    SID : 17e43a200d0f4ea8668f43a2e43344a1
      mode : Authenticated
      sender-ip/port : 1.1.1.11/20000
      receiver-ip/port : 1.1.1.12/20000
      test-aes-session-key : 57d469962fe97183378eb584df0d4bed
      test-hmac-sha1-session-key : 3c18a35a111f2918a69080de5adf22a16d90a54d37df332afd99d6c6a65d0ae9


3.4. 	< show twamp sender > command
3.4.1	< show twamp sender status > command
show service twamp sender status
Show twamp sender parameters.

show twamp sender
show twamp sender status

Syntax Description
None

Default
None

Command Modes
System Execution Mode

Example
N1(exec)#show twamp sender 
twamp sender
  test-session TEST-N2
    control-connection-name is CONN-N2
    fill-mode : zero
    number-of-packet : 1000000
    interval : 1 seconds


3.4.2	< show twamp sender session > command
show service twamp session
Show all session’s information of twamp sender

show twamp sender session

Syntax Description
None

Default
None

Command Modes
System Execution Mode

Example
N1(exec)#show twamp sender session 
twamp sender
  test-session TEST-N2
    control-connection-name is CONN-N2
  test-session TEST-N3
    control-connection-name is CONN-N3
  test-session TEST-N4
control-connection-name is CONN-N4


3.4.3	< show twamp sender session WORD> command
show service twamp session WORD
Show detail information of specific twamp session

show twamp sender session WORD

Syntax Description
WROD
Twamp test-session name
Default
None

Command Modes
System Execution Mode

Example
N1(exec)#show twamp sender session TEST-N2
test-session TEST-N2
  control-connection-name : CONN-N2
  fill-mode : zero
  number-of-packet : 1000000
  interval : 1 seconds
  session-request : SESS-01
    operation status : active
    received/sent packets : 11078/11078
    last received/sent sequence : 11077/11077
    mean rtt : 0 sec 905 usec
    stdev rtt : 0 sec 69 usec
    ipdv variation : 0 sec 91 usec
      lowest variation : 0 sec -1303 usec
      highestest variation : 0 sec 1608 usec
    pdv variation : 0 sec 464 usec
      lowest rtt : 0 sec 494 usec
      max variation : 0 sec 1761 usec


3.5. 	< twping > command
3.5.1	<twping A.B.C.D > command
twping A.B.C.D
A.B.C.D : Reflector ipv4 address.

twping A.B.C.D count <1-100>
A.B.C.D 	: Reflector ipv4 address.
count 	: number of test packet.

twping A.B.C.D count <1-100> reflector-port <100-65535>
A.B.C.D 	: Reflector ipv4 address.
count 	: number of test packet.
reflector-port	: upd port of reflector

twping A.B.C.D mode (unauthenticated|authenticated|encrypted|mixed) key-id WORD secret-key WORD
A.B.C.D 	: Reflector ipv4 address.
mode 	: unauthenticated|authenticated|encrypted|mixed
key-id	: string value of key-id
secret-key	: string value of passphrase

twping A.B.C.D server-tcp-port <100-65535> mode (unauthenticated|authenticated|encrypted|mixed) key-id WORD secret-key WORD
A.B.C.D 	: Reflector ipv4 address.
server-tcp-port	: tcp port of server
mode 	: unauthenticated|authenticated|encrypted|mixed
key-id	: string value of key-id
secret-key	: string value of passphrase

twping A.B.C.D count <1-100> mode (unauthenticated|authenticated|encrypted|mixed) key-id WORD secret-key WORD
A.B.C.D 	: Reflector ipv4 address.
count 	: number of test packet.
mode 	: unauthenticated|authenticated|encrypted|mixed
key-id	: string value of key-id
secret-key	: string value of passphrase

twping A.B.C.D count <1-100> server-tcp-port <100-65535> mode (unauthenticated|authenticated|encrypted|mixed) key-id WORD secret-key WORD
A.B.C.D 	: Reflector ipv4 address.
count 	: number of test packet.
server-tcp-port	: tcp port of server
mode 	: unauthenticated|authenticated|encrypted|mixed
key-id	: string value of key-id
secret-key	: string value of passphrase

twping A.B.C.D count <1-100> session-count <2-100> mode (unauthenticated|authenticated|encrypted|mixed) key-id WORD secret-key WORD
A.B.C.D 	: Reflector ipv4 address.
count 	: number of test packet.
session-count	: number of test sessions
mode 	: unauthenticated|authenticated|encrypted|mixed
key-id	: string value of key-id
secret-key	: string value of passphrase

twping A.B.C.D count <1-100> session-count <2-100> server-tcp-port <100-65535> mode (unauthenticated|authenticated|encrypted|mixed) key-id WORD secret-key WORD
A.B.C.D 	: Reflector ipv4 address.
count 	: number of test packet.
session-count	: number of test sessions
server-tcp-port	: tcp port of server
mode 	: unauthenticated|authenticated|encrypted|mixed
key-id	: string value of key-id
secret-key	: string value of passphrase

Command Modes
System Execution Mode

Example
Twping with TWAMP Light Server
<< twping A.B.C.D >>
N1(exec)# twping 1.1.1.12

<< twping A.B.C.D count <1-100> >>
N1(exec)# twping 1.1.1.12 count 10

<< twping A.B.C.D reflector-port <100-65535> >>
N1(exec)# twping 1.1.1.12 reflector-port 863

<< twping A.B.C.D count <1-100> reflector-port <100-65535> >>
N1(exec)# twping 1.1.1.12 count 10 reflector-port 863

Twping with TWAMP Full Server
<<twping A.B.C.D mode (unauthenticated|authenticated|encrypted|mixed) key-id WORD secret-key WORD>>
N1(exec)# twping 1.1.1.12 mode unauthenticated key-id user01 secret-key password01
N1(exec)# twping 1.1.1.12 mode authenticated key-id user01 secret-key password01
N1(exec)# twping 1.1.1.12 mode encrypted key-id user01 secret-key password01
N1(exec)# twping 1.1.1.12 mode mixed key-id user01 secret-key password01

<<twping A.B.C.D count <2-100> mode (unauthenticated|authenticated|encrypted|mixed) key-id WORD secret-key WORD>>
N1(exec)# twping 1.1.1.12 count 5 mode unauthenticated key-id user01 secret-key password01
N1(exec)# twping 1.1.1.12 count 5 mode authenticated key-id user01 secret-key password01
N1(exec)# twping 1.1.1.12 count 5 mode encrypted key-id user01 secret-key password01
N1(exec)# twping 1.1.1.12 count 5 mode mixed key-id user01 secret-key password01

<<twping A.B.C.D count <2-100> session-count <2-100> mode (unauthenticated|authenticated|encrypted|mixed) key-id WORD secret-key WORD>>
N1(exec)# twping 1.1.1.12 count 5 session-count 5 mode unauthenticated key-id user01 secret-key password01
N1(exec)# twping 1.1.1.12 count 5 session-count 5 mode authenticated key-id user01 secret-key password01
N1(exec)# twping 1.1.1.12 count 5 session-count 5 mode encrypted key-id user01 secret-key password01
N1(exec)# twping 1.1.1.12 count 5 session-count 5 mode mixed key-id user01 secret-key password01

<<twping A.B.C.D server-tcp-port <100-65535> mode (unauthenticated|authenticated|encrypted|mixed) key-id WORD secret-key WORD>>
N1(exec)# twping 1.1.1.12 server-port 863 mode unauthenticated user user01 password password01
N1(exec)# twping 1.1.1.12 server-port 863 mode authenticated user user01 password password01
N1(exec)# twping 1.1.1.12 server-port 863 mode encrypted user user01 password password01
N1(exec)# twping 1.1.1.12 server-port 863 mode mixed user user01 password password01

<<twping A.B.C.D count <1-100> server-tcp-port <100-65535> mode (unauthenticated|authenticated|encrypted|mixed) key-id WORD secret-key WORD>>
N1(exec)# twping 1.1.1.12 count 5 server-port 863 mode unauthenticated user user01 password password01
N1(exec)# twping 1.1.1.12 count 5 server-port 863 mode authenticated user user01 password password01
N1(exec)# twping 1.1.1.12 count 5 server-port 863 mode encrypted user user01 password password01
N1(exec)# twping 1.1.1.12 count 5 server-port 863 mode mixed user user01 password password01

<<twping A.B.C.D count <1-100> session-count <2-100> server-tcp-port <100-65535> mode (unauthenticated|authenticated|encrypted|mixed) key-id WORD secret-key WORD>>
N1(exec)# twping 1.1.1.12 count 5 session-count 5 server-port 863 mode unauthenticated user user01 password password01
N1(exec)# twping 1.1.1.12 count 5 session-count 5 server-port 863 mode authenticated user user01 password password01
N1(exec)# twping 1.1.1.12 count 5 session-count 5 server-port 863 mode encrypted user user01 password password01
N1(exec)# twping 1.1.1.12 count 5 session-count 5 server-port 863 mode mixed user user01 password password01

Welcome to StackEdit!
===================


Hey! I'm your first Markdown document in **StackEdit**[^stackedit]. Don't delete me, I'm very helpful! I can be recovered anyway in the **Utils** tab of the <i class="icon-cog"></i> **Settings** dialog.

----------


Documents
-------------

StackEdit stores your documents in your browser, which means all your documents are automatically saved locally and are accessible **offline!**

> **Note:**

> - StackEdit is accessible offline after the application has been loaded for the first time.
> - Your local documents are not shared between different browsers or computers.
> - Clearing your browser's data may **delete all your local documents!** Make sure your documents are synchronized with **Google Drive** or **Dropbox** (check out the [<i class="icon-refresh"></i> Synchronization](#synchronization) section).

#### <i class="icon-file"></i> Create a document

The document panel is accessible using the <i class="icon-folder-open"></i> button in the navigation bar. You can create a new document by clicking <i class="icon-file"></i> **New document** in the document panel.

#### <i class="icon-folder-open"></i> Switch to another document

All your local documents are listed in the document panel. You can switch from one to another by clicking a document in the list or you can toggle documents using <kbd>Ctrl+[</kbd> and <kbd>Ctrl+]</kbd>.

#### <i class="icon-pencil"></i> Rename a document

You can rename the current document by clicking the document title in the navigation bar.

#### <i class="icon-trash"></i> Delete a document

You can delete the current document by clicking <i class="icon-trash"></i> **Delete document** in the document panel.

#### <i class="icon-hdd"></i> Export a document

You can save the current document to a file by clicking <i class="icon-hdd"></i> **Export to disk** from the <i class="icon-provider-stackedit"></i> menu panel.

> **Tip:** Check out the [<i class="icon-upload"></i> Publish a document](#publish-a-document) section for a description of the different output formats.


----------


Synchronization
-------------------

StackEdit can be combined with <i class="icon-provider-gdrive"></i> **Google Drive** and <i class="icon-provider-dropbox"></i> **Dropbox** to have your documents saved in the *Cloud*. The synchronization mechanism takes care of uploading your modifications or downloading the latest version of your documents.

> **Note:**

> - Full access to **Google Drive** or **Dropbox** is required to be able to import any document in StackEdit. Permission restrictions can be configured in the settings.
> - Imported documents are downloaded in your browser and are not transmitted to a server.
> - If you experience problems saving your documents on Google Drive, check and optionally disable browser extensions, such as Disconnect.

#### <i class="icon-refresh"></i> Open a document

You can open a document from <i class="icon-provider-gdrive"></i> **Google Drive** or the <i class="icon-provider-dropbox"></i> **Dropbox** by opening the <i class="icon-refresh"></i> **Synchronize** sub-menu and by clicking **Open from...**. Once opened, any modification in your document will be automatically synchronized with the file in your **Google Drive** / **Dropbox** account.

#### <i class="icon-refresh"></i> Save a document

You can save any document by opening the <i class="icon-refresh"></i> **Synchronize** sub-menu and by clicking **Save on...**. Even if your document is already synchronized with **Google Drive** or **Dropbox**, you can export it to a another location. StackEdit can synchronize one document with multiple locations and accounts.

#### <i class="icon-refresh"></i> Synchronize a document

Once your document is linked to a <i class="icon-provider-gdrive"></i> **Google Drive** or a <i class="icon-provider-dropbox"></i> **Dropbox** file, StackEdit will periodically (every 3 minutes) synchronize it by downloading/uploading any modification. A merge will be performed if necessary and conflicts will be detected.

If you just have modified your document and you want to force the synchronization, click the <i class="icon-refresh"></i> button in the navigation bar.

> **Note:** The <i class="icon-refresh"></i> button is disabled when you have no document to synchronize.

#### <i class="icon-refresh"></i> Manage document synchronization

Since one document can be synchronized with multiple locations, you can list and manage synchronized locations by clicking <i class="icon-refresh"></i> **Manage synchronization** in the <i class="icon-refresh"></i> **Synchronize** sub-menu. This will let you remove synchronization locations that are associated to your document.

> **Note:** If you delete the file from **Google Drive** or from **Dropbox**, the document will no longer be synchronized with that location.

----------


Publication
-------------

Once you are happy with your document, you can publish it on different websites directly from StackEdit. As for now, StackEdit can publish on **Blogger**, **Dropbox**, **Gist**, **GitHub**, **Google Drive**, **Tumblr**, **WordPress** and on any SSH server.

#### <i class="icon-upload"></i> Publish a document

You can publish your document by opening the <i class="icon-upload"></i> **Publish** sub-menu and by choosing a website. In the dialog box, you can choose the publication format:

- Markdown, to publish the Markdown text on a website that can interpret it (**GitHub** for instance),
- HTML, to publish the document converted into HTML (on a blog for example),
- Template, to have a full control of the output.

> **Note:** The default template is a simple webpage wrapping your document in HTML format. You can customize it in the **Advanced** tab of the <i class="icon-cog"></i> **Settings** dialog.

#### <i class="icon-upload"></i> Update a publication

After publishing, StackEdit will keep your document linked to that publication which makes it easy for you to update it. Once you have modified your document and you want to update your publication, click on the <i class="icon-upload"></i> button in the navigation bar.

> **Note:** The <i class="icon-upload"></i> button is disabled when your document has not been published yet.

#### <i class="icon-upload"></i> Manage document publication

Since one document can be published on multiple locations, you can list and manage publish locations by clicking <i class="icon-upload"></i> **Manage publication** in the <i class="icon-provider-stackedit"></i> menu panel. This will let you remove publication locations that are associated to your document.

> **Note:** If the file has been removed from the website or the blog, the document will no longer be published on that location.

----------


Markdown Extra
--------------------

StackEdit supports **Markdown Extra**, which extends **Markdown** syntax with some nice features.

> **Tip:** You can disable any **Markdown Extra** feature in the **Extensions** tab of the <i class="icon-cog"></i> **Settings** dialog.

> **Note:** You can find more information about **Markdown** syntax [here][2] and **Markdown Extra** extension [here][3].


### Tables

**Markdown Extra** has a special syntax for tables:

Item     | Value
-------- | ---
Computer | $1600
Phone    | $12
Pipe     | $1

You can specify column alignment with one or two colons:

| Item     | Value | Qty   |
| :------- | ----: | :---: |
| Computer | $1600 |  5    |
| Phone    | $12   |  12   |
| Pipe     | $1    |  234  |


### Definition Lists

**Markdown Extra** has a special syntax for definition lists too:

Term 1
Term 2
:   Definition A
:   Definition B

Term 3

:   Definition C

:   Definition D

	> part of definition D


### Fenced code blocks

GitHub's fenced code blocks are also supported with **Highlight.js** syntax highlighting:

```
// Foo
var bar = 0;
```

> **Tip:** To use **Prettify** instead of **Highlight.js**, just configure the **Markdown Extra** extension in the <i class="icon-cog"></i> **Settings** dialog.

> **Note:** You can find more information:

> - about **Prettify** syntax highlighting [here][5],
> - about **Highlight.js** syntax highlighting [here][6].


### Footnotes

You can create footnotes like this[^footnote].

  [^footnote]: Here is the *text* of the **footnote**.


### SmartyPants

SmartyPants converts ASCII punctuation characters into "smart" typographic punctuation HTML entities. For example:

|                  | ASCII                        | HTML              |
 ----------------- | ---------------------------- | ------------------
| Single backticks | `'Isn't this fun?'`            | 'Isn't this fun?' |
| Quotes           | `"Isn't this fun?"`            | "Isn't this fun?" |
| Dashes           | `-- is en-dash, --- is em-dash` | -- is en-dash, --- is em-dash |


### Table of contents

You can insert a table of contents using the marker `[TOC]`:

[TOC]


### MathJax

You can render *LaTeX* mathematical expressions using **MathJax**, as on [math.stackexchange.com][1]:

The *Gamma function* satisfying $\Gamma(n) = (n-1)!\quad\forall n\in\mathbb N$ is via the Euler integral

$$
\Gamma(z) = \int_0^\infty t^{z-1}e^{-t}dt\,.
$$

> **Tip:** To make sure mathematical expressions are rendered properly on your website, include **MathJax** into your template:

```
<script type="text/javascript" src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS_HTML"></script>
```

> **Note:** You can find more information about **LaTeX** mathematical expressions [here][4].


### UML diagrams

You can also render sequence diagrams like this:

```sequence
Alice->Bob: Hello Bob, how are you?
Note right of Bob: Bob thinks
Bob-->Alice: I am good thanks!
```

And flow charts like this:

```flow
st=>start: Start
e=>end
op=>operation: My Operation
cond=>condition: Yes or No?

st->op->cond
cond(yes)->e
cond(no)->op
```

> **Note:** You can find more information:

> - about **Sequence diagrams** syntax [here][7],
> - about **Flow charts** syntax [here][8].

### Support StackEdit

[![](https://cdn.monetizejs.com/resources/button-32.png)](https://monetizejs.com/authorize?client_id=ESTHdCYOi18iLhhO&summary=true)

  [^stackedit]: [StackEdit](https://stackedit.io/) is a full-featured, open-source Markdown editor based on PageDown, the Markdown library used by Stack Overflow and the other Stack Exchange sites.


  [1]: http://math.stackexchange.com/
  [2]: http://daringfireball.net/projects/markdown/syntax "Markdown"
  [3]: https://github.com/jmcmanus/pagedown-extra "Pagedown Extra"
  [4]: http://meta.math.stackexchange.com/questions/5020/mathjax-basic-tutorial-and-quick-reference
  [5]: https://code.google.com/p/google-code-prettify/
  [6]: http://highlightjs.org/
  [7]: http://bramp.github.io/js-sequence-diagrams/
  [8]: http://adrai.github.io/flowchart.js/
