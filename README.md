<h1>Network configuration</h1>

<pre>
+---------+
|    N1   |192.168.122.101
+---------+
     | 1.1.1.11         1.1.1.12  +---------+
     |----------------------------|    N2   |192.168.122.102
     |                            +---------+
     | 2.2.2.11         2.2.2.12  +---------+
     |----------------------------|    N3   |192.168.122.103
     |                            +---------+
     | 3.3.3.11         3.3.3.12  +---------+
     |----------------------------|    N4   |192.168.122.104
     |                            +---------+
</pre>

<h1>TWAMP Configuration<h1>

<h3>N2, N3, N4 configuration : Twamp server and reflector<h3>
<pre>
!
twamp server
	key-chain
		key-id key01 secret-key secret01
		key-id key02 secret-key secret02
		key-id key03 secret-key secret03
	mode unauthenticated authenticated encrypted mixed
	control-packet-dscp 0
	maximum-connections 10
	maximum-sessions-per-connection 10
	server-tcp-port 862
	count 1024
	base-test-port 20000
	serv-ref-wait 30
!
</pre>

<h3>N1 configuration : Twamp client and sender

<pre>
!
twamp client
	monitor
		listen-tcp-port 22222
		max-connection 4
		client-ip 192.168.122.101
		client-ip 192.168.122.102
	mode-preference
		priority 0 mode authenticated
		priority 1 mode encrypted
		priority 2 mode mixed
	key-chain
		key-id key01 secret-key secret01
	control-connection CONN-N2
		client-ip 192.168.122.101
		server-ip 192.168.122.102
		key-id key01
		session-request SESS-01
			sender-ip 1.1.1.11
			reflector-ip 1.1.1.12
	control-connection CONN-N3
		client-ip 192.168.122.101
		server-ip 192.168.122.103
		key-id key01
		session-request SESS-01
			sender-ip 2.2.2.11
			reflector-ip 2.2.2.13
	control-connection CONN-N4
		client-ip 192.168.122.101
		server-ip 192.168.122.104
		key-id key01
		session-request SESS-01
			sender-ip 3.3.3.11
			reflector-ip 3.3.3.14
!
twamp sender
	test-session TEST-N2
		control-connection-name CONN-N2
		number-of-packet 1000000

        test-session TEST-N3
		control-connection-name CONN-N3
		number-of-packet 1000000
	test-session TEST-N4
		control-connection-name CONN-N4
		number-of-packet 1000000
!
</pre>

<h3>Start twamp control and test sessions

<pre>
N1(exec)#twping start sender-test-session TEST-N2
N1(exec)#twping start sender-test-session TEST-N2
N1(exec)#twping start sender-test-session TEST-N3
</pre>

<h3>how to run monitor client program

<pre>
root@N1:~# cd ~~~/twampd/sample
root@N1:~~~/twampd/sample# make
root@N1:~~~/twampd/sample# ./mon-client 192.168.122.101 22222
Connect to : 192.168.122.101/22222
Connected (local : 192.168.122.101/36214, server : 192.168.122.101/22222)
[192.168.122.101:34850, 192.168.122.102:862]
    RecvPackets/SentPackets     : 4456/4456
    LastRecvSeq/LastSentSeq     : 4455/4455
    CurrentDrop/AccumulatedDrop : 0/0
    CurrentRtt                  : 0 Sec 751 USec
    MeanRtt                     : 0 Sec 967 USec
    StdDevRtt                   : 0 Sec 319 USec
    IPDV (lowest ~ highest)     : 0 Sec -203 USec(0 Sec -6129 USec ~ 0 Sec 5990 USec)
    PDV (low-rtt, max-variation): 0 Sec 295 USec(0 Sec 456 USec, 0 Sec 6555 USec)
    Duplicated(*)               : 0
    Disordered(*)               : 0
</pre>

----

<h1>
TWAMP Command

<h2> 1.	Configuration Mode Command

<h3> 1.1 twamp light command
<h5> twamp light

<pre>Start the TWAMP light server. By default, the server receive and response twamp-test packets from any client.</pre>

<pre>(no) twamp light</pre>

<h5> Syntax Description
<pre>None </pre>

<h5> Default
<pre>Default is “no twamp light”. </pre>

<h5> Command Modes
<pre>System Configuration Mode </pre>

<h5> Example
<pre>N1(config)# twamp light
N1(config)# no twamp light </pre>

<h3>1.1.1 reflector-port command
<h5>reflector-port
<pre>reflector udp port that receive and response twamp-test packets from any client.</pre>
<pre>reflector-port [100-100000]
no reflector-port</pre>

<h5>Syntax Description
<pre>None</pre>

<h5>Default
<pre>Default is 862.</pre>

<h5>Command Modes
<pre>Twamp light Mode</pre>

<h5>Example
<pre>N1(config)# twamp light
N1(twamp-light)# reflector-port 1000
N1(twamp-light)# no reflector-port</pre>


<h3>1.2 twamp server command
<h5>twamp server
<pre>Start the TWAMP server. By default, the server accepts any connection request from any client.</pre>

<pre>(no) twamp server</pre>

<h5>Syntax Description
<pre>None</pre>

<h5>Default
<pre>Default is “no twamp server”.</pre>

<h5>Command Modes
<pre>System Configuration Mode</pre>

<h5>Example
<pre>N1(config)# twamp server
N1(config)# no twamp server</pre>


<h3>1.2.1 control-packet-dscp command
<h5>control-packet-dscp
<pre>Specify value as the DSCP byte in the IP header of control packets sent from the server.</pre>

<pre>(no) control-packet-dscp [0-255]</pre>

<h5>Syntax Description
<pre>[0-255]
	DSCP value</pre>

<h5>Default
<pre>Default is ”0”.</pre>

<h5>Command Modes
<pre>Twamp server mode</pre>

<h5>Example
<pre>N1(config)# twamp server
N1(twamp-server)# control-packet-dscp 12
N1(twamp-server)# no control-packet-dscp</pre>

<pre>[Note] DSCP Rule(control and test packet)
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
255	11111111	252	11111100</pre>


<h3>1.2.2 maximum-connections command
<h5>Server maximum-connections
<pre>Specify value as the maximum number of control sessions for each TWAMP server.</pre>

<pre>(no) maximum-connections [1-100]</pre>

<h5>Syntax Description
<pre>[1-100] Maximum connections value default 10</pre>

<h5>Default
<pre>Default is “10”.</pre>

<h5>Command Modes
<pre>Twamp server mode</pre>

<h5>Example
<pre>N1(config)# twamp server
N1(twamp-server)# maximum-connections 11
N1(twamp-server)# no maximum-connections</pre>


<h3>1.2.3 maximum-sessions-per-connection command
<h5>maximum-sessions-per-connection
<pre>Limit the number of maximum number of test sessions for each control session.</pre>

<pre>(no) maximum-sessions-per-connection 1-100]</pre>

<h5>Syntax Description
<pre>[1-100] 
	the number of maximum number of test sessions for each control session</pre>

<h5>Default
<pre>Default is ”10”.</pre>

<h5>Command Modes
<pre>Twamp server mode</pre>

<h5>Example
<pre>N1(config)# twamp server
N1(twamp-server)# maximum-sessions-per-connection 11
N1(twamp-server)# no maximum-sessions-per-connection</pre>


<h3>1.2.4 mode command
<h5>server mode
<pre>Enable security mode.</pre>

<pre>(no) mode {unauthenticated | authenticated | encrypted | mixed}</pre>

<h5>Syntax Description
<pre>unauthenticated
	unauthenticated mode
authenticated
	authenticated mode
encrypted
	encrypted mode
mixed
	control packets are encrypted and test packets are unauthenticated.</pre>

<h5>Default
<pre>Default is "unauthenticated mode".</pre>

<h5>Command Modes
<pre>Twamp server mode</pre>

<h5>Example
<pre>N1(config)# twamp server
N2(twamp-server)# mode unauthenticated authenticated encrypted mixed
N2(twamp-server)# no mode unauthenticated authenticated encrypted mixed</pre>


<h3>1.2.5 server-tcp-port command
<h5>server-tcp-port
<pre>Specify number as the TCP port used for control sessions.</pre>

<pre>server-tcp-port [100-100000]
no server-tcp-port</pre>

<h5>Syntax Description
<pre>[100-100000]
	number as the TCP port</pre>

<h5>Default
<pre>Default is “862”.</pre>

<h5>Command Modes
<pre>Twamp server mode</pre>

<h5>Example
<pre>N1(config)# 
N1(twamp-server)# server-tcp-port 862
N1(twamp-server)# no server-tcp-port</pre>


<h3>1.2.6 max-count command
<h5>Max-count
<pre>This parameter limits the maximum Count value.</pre>

<pre>max-count [1024-32768]
no max-count</pre>

<h5>Syntax Description
<pre>[1024-32768]
	Count value for deriving key. default 32768</pre>

<h5>Default
<pre>Default is “32768”.</pre>

<h5>Command Modes
<pre>Twamp server mode</pre>

<h5>Example
<pre>N1(config)# 
N1(twamp-server)# max-count 1024
N1(twamp-server)# no max-count</pre>


<h3>1.2.7 count command
<h5>count
<pre>Parameter used in deriving a key from a shared secret as described in Section 3.1 of RFC 4656, and are communicated to the Control-Client as part of the Server Greeting message.</pre>

<pre>count [1024-32768]
no count</pre>

<h5>Syntax Description
<pre>[1024-32768]
	Count value for deriving key. default 1024</pre>

<h5>Default
<pre>Default is “1024”.</pre>

<h5>Command Modes
<pre>Twamp server mode</pre>

<h5>Example
<pre>N1(config)# 
N1(twamp-server)# count 1024
N1(twamp-server)# no count</pre>


<h3>1.2.8 base-test-port command
<h5>Max-count
<pre>This parameter is the value of dynamic allocated UDP port of test packet.</pre>

<pre>base-test-port [1024-65535]
no base-test-port</pre>

<h5>Syntax Description
<pre>[1024-65535]
	UDP port number. default 20000</pre>

<h5>Default
<pre>Default is “20000”.</pre>

<h5>Command Modes
<pre>Twamp server mode</pre>

<h5>Example
<pre>N1(config)# 
N1(twamp-server)# base-test-port 20001
N1(twamp-server)# no base-test-port</pre>


<h3>1.2.9 serv-ref-wait command
<h5>servwait
<pre>Set the timeout value for control-session inactivity in seconds. Indicates that the TWAMP-Control connection to the Control-Client is in SERVWAIT according to RFC 5357 (Section 3.1): [a] Server MAY discontinue any established control connection when no packet associated with that connection has been received within SERVWAIT seconds.</pre>

<pre>servwait [1-604800]
no servwait</pre>

<h5>Syntax Description
<pre>[1-604800]
	timeout value for control-session</pre>

<h5>Default
<pre>Default is “900”.</pre>

<h5>Command Modes
<pre>Twamp server mode</pre>

<h5>Example
<pre>N1(config)# twamp server
N1(twamp-server)# serv-ref-wait 100
N1(twamp-server)# no serv-ref-wait 100</pre>


<h3>1.2.10 key-chain command
<h5>key-chain
<pre>Enter key-chain mode.</pre>

<pre>(no) key-chain</pre>

<h5>Syntax Description
<pre>None</pre>

<h5>Default
<pre>None</pre>

<h5>Command Modes
<pre>Twamp server mode</pre>

<h5>Example
<pre>N1(twamp-server)# key-chain
N1(twamp-server)# no key-chain</pre>


<h3>1.2.11 key-id command
<h5>key-id
<pre>Set key-id and secure-key</pre>

<pre>key-id WORD secret-key WORD
no key-id WORD</pre>

<h5>Syntax Description
<pre>Key-id
	string for key-name
secure-key
	string for passprase</pre>

<h5>Default
<pre>None</pre>

<h5>Command Modes
<pre>Twamp server key-chain mode</pre>

<h5>Example
<pre>N1(twamp-server-key-chain)# key-id KEY01 secure-id SECURE01
N1(twamp-server-key-chain)# no key-id</pre>


<h3>1.3 twamp client command
<h5>twamp client
<pre>Enter the TWAMP client configuration mode. </pre>

<pre>(no) twamp client</pre>

<h5>Syntax Description
<pre>None</pre>

<h5>Default
<pre>Default is “no twamp client”.</pre>

<h5>Command Modes
<pre>System Configuration Mode</pre>

<h5>Example
<pre>N1(config)# twamp client
N1(config)# no twamp client</pre>


<h3>1.3.1 mode-preference command
<h5>mode-preference
<pre>Enter “twamp client mode-preference” mode. </pre>

<pre>(no) mode-preference</pre>

<h5>Syntax Description
<pre>None</pre>

<h5>Default
<pre>None</pre>

<h5>Command Modes
<pre>Twamp client mode</pre>

<h5>Example
<pre>N1(twamp-client)# mode-preference
N1(twamp-client)# no mode-preference</pre>

<h3>1.3.1.1 priority command
<h5>priority
<pre>Specify value as the DSCP byte in the IP header of control packets sent from the server.</pre>

<pre>(no) priority [0-3] mode (unauthenticated|authenticated|encrypted|mixed)</pre>

<h5>Syntax Description
<pre>[0-3]
	Mode priority
unauthenticated|authenticated|encrypted|mixed
	Supported TWAMP Mode.</pre>

<h5>Default
<pre>Default is "unauthenticated".</pre>

<h5>Command Modes
<pre>Twamp client mode-preference mode</pre>

<h5>Example
<pre>N1(config)# twamp server
N1(twamp-client)# mode-preference
N1(twamp-client-mode-prefer)# priority 0 mode unauthenticated
N1(twamp-client-mode-prefer)# priority 1 mode authenticated
N1(twamp-client-mode-prefer)# priority 2 mode encrypted
N1(twamp-client-mode-prefer)# priority 3 mode mixed
N1(twamp-client-mode-prefer)# no priority 0
N1(twamp-client-mode-prefer)# no priority 1
N1(twamp-client-mode-prefer)# no priority 2
N1(twamp-client-mode-prefer)# no priority 3</pre>

<h3>1.3.2 key-chain command
<h5>key-chain
<pre>Enter “twamp client key-chain” mode. </pre>

<pre>(no) key-chain</pre>

<h5>Syntax Description
<pre>None</pre>

<h5>Default
<pre>None</pre>

<h5>Command Modes
<pre>Twamp client mode</pre>

<h5>Example
<pre>N1(twamp-client)# key-chain
N1(twamp-client)# no key-chain</pre>


<h3>1.3.2.1 key-id command
<h5>key-id
<pre>Set key-id and secure-key</pre>

<pre>(no) key-id WORD secret-key WORD</pre>

<h5>Syntax Description
<pre>Key-id
	string for key-name
secure-key
	string for passprase</pre>

<h5>Default
<pre>None</pre>

<h5>Command Modes
<pre>Twamp client key-chain mode</pre>

<h5>Example
<pre>N1(twamp-server-key-chain)# key-id KEY01 secure-id SECURE01
N1(twamp-server-key-chain)# no key-id KEY01</pre>


<h3>1.3.3 control-connection command
<h5>control-connection
<pre>Enter “twamp client control-connection” mode. </pre>

<pre>(no) control-connection WORD</pre>

<h5>Syntax Description
<pre>WORD
	String for control-connection name</pre>

<h5>Default
<pre>None</pre>

<h5>Command Modes
<pre>Twamp client mode</pre>

<h5>Example
<pre>N1(twamp-client)# control-connection CONN-01
N1(twamp-client)# no control-connection CONN-01</pre>

<h3>1.3.3.1 client-ip command
<h5>client-ip
<pre>Set client ip address for twamp control.</pre>

<pre>client-ip A.B.C.D
no client-ip</pre>

<h5>Syntax Description
<pre>A.B.C.D
	Ipv4 address format</pre>

<h5>Default
<pre>None</pre>

<h5>Command Modes
<pre>Twamp client control-connection mode</pre>

<h5>Example
<pre>N1(twamp-client-ctrl-conn)# client-ip 1.1.1.1
N1(twamp-client-ctrl-conn)# no client-ip</pre>


<h3>1.3.3.2 server-ip command
<h5>server-ip
<pre>Set server ip address for twamp control.</pre>

<pre>server-ip A.B.C.D
no server</pre>

<h5>Syntax Description
<pre>A.B.C.D
	Ipv4 address format</pre>

<h5>Default
<pre>None</pre>

<h5>Command Modes
<pre>Twamp client control-connection mode</pre>

<h5>Example
<pre>N1(twamp-client-ctrl-conn)# server-ip 1.1.1.1
N1(twamp-client-ctrl-conn)# no server-ip</pre>

<h3>1.3.3.3 server-tcp-port command
<h5>server-tcp-port
<pre>Set server control tcp port for twamp control.</pre>

<pre>server-tcp-port [100-65535]
no server-tcp-port</pre>

<h5>Syntax Description
<pre>[100-65535]
	server tcp port number</pre>

<h5>Default
<pre>Default is "862"</pre>

<h5>Command Modes
<pre>Twamp client control-connection mode</pre>

<h5>Example
<pre>N1(twamp-client-ctrl-conn)# server-tcp-port 863
N1(twamp-client-ctrl-conn)# no server-tcp-port</pre>


<h3>1.3.3.4 control-packet-dscp command
<h5>control-packet-dscp
<pre>Set dscp value for control connection. The DSCP value to be placed in the IP header of TWAMP-Control (TCP) packets generated by this Control-Client.</pre>

<pre>control-packet-dscp [0-255]
no control-packet-dscp</pre>

<h5>Syntax Description
<pre>[0-255]
	dscp value</pre>

<h5>Default
<pre>Default is "0"</pre>

<h5>Command Modes
<pre>Twamp client control-connection mode</pre>

<h5>Example
<pre>N1(twamp-client-ctrl-conn)# control-packet-dscp 5
N1(twamp-client-ctrl-conn)# no control-packet-dscp</pre>


<h3>1.3.3.5 key-id command
<h5>control-packet-dscp
<pre>Set key-id string for control connection. The KeyID value that is selected for this TWAMP-Control connection.</pre>

<pre>key-id WORD
no key-id</pre>

<h5>Syntax Description
<pre>WORD
	String value for key-id</pre>

<h5>Default
<pre>None</pre>

<h5>Command Modes
<pre>Twamp client control-connection mode</pre>

<h5>Example
<pre>N1(twamp-client-ctrl-conn)# key-id KEY-01
N1(twamp-client-ctrl-conn)# no key-id</pre>


<h3>1.3.3.6 max-count command
<h5>max-count
<pre>Set max-count for count. This parameter limits the maximum Count value. If an attacking system sets the maximum value in Count (2**32), then the system under attack would stall for a significant period of time while it attempts to generate keys.</pre>

<pre>max-count [1024-32768]
no max-count</pre>

<h5>Syntax Description
<pre>[1024-32768]
	Maximum value for count.</pre>

<h5>Default
<pre>Default is "32768"</pre>

<h5>Command Modes
<pre>Twamp client control-connection mode</pre>

<h5>Example
<pre>N1(twamp-client-ctrl-conn)# max-count 2048
N1(twamp-client-ctrl-conn)# no max-count</pre>


<h3>1.3.3.7 session-request command
<h5>session-request
<pre>Enter “twamp client control-connection session-request” mode. Information associated with the Control-Client for this test session</pre>

<pre>(no) session-request WORD</pre>

<h5>Syntax Description
<pre>WORD
	String for session-request name</pre>

<h5>Default
<pre>None</pre>

<h5>Command Modes
<pre>Twamp client control-connection mode</pre>

<h5>Example
<pre>N1(twamp-client-control-connection)# session-request SESS-REQ-01
N1(twamp-client-control-connection)# no session-request SESS-REQ-01</pre>


<h3>1.3.3.7.1 sender-ip command
<h5>sender-ip
<pre>Set sender ip address for twamp test. The IP address of the Session-Sender device, which is to be placed in the source IP address field of the IP header in TWAMP-Test (UDP) packets belonging to this test session. This value will be used to populate the sender address field of the Request-TW-Session message. If not configured, the device SHALL choose its own source IP address.</pre>

<pre>sender-ip A.B.C.D
no sender-ip</pre>

<h5>Syntax Description
<pre>A.B.C.D
	Ipv4 address format</pre>

<h5>Default
<pre>None</pre>

<h5>Command Modes
<pre>Twamp client control-connection session-request mode</pre>

<h5>Example
<pre>N1(twamp-client-session-request)# sender-ip 1.1.1.1
N1(twamp-client-session-request)# no sender-ip</pre>

<h3>1.3.3.7.2 sender-udp-port command
<h5>sender-udp-port
<pre>Set sender udp port for twamp test. The UDP port number that is to be used by the Session-Sender for this TWAMP-Test session. The number is restricted to the dynamic port range. A value of zero indicates that the Control-Client SHALL auto-allocate a UDP port number for this TWAMP-Test session. The configured (or auto-allocated) value is advertized in the Sender Port field of the Request-TW-session message (see also Section 3.5 of RFC 5357. Note that in the scenario where a device auto-allocates a UDP port number for a session, and the repeat parameter for that session indicates that it should be repeated, the device is free to auto-allocate a different UDP port number when it negotiates the next (repeated) iteration of this session.</pre>

<pre>sender-udp-port [100-65535]
no sender-udp-port</pre>

<h5>Syntax Description
<pre>[100-65535]
	Sender udp port.</pre>

<h5>Default
<pre>None</pre>

<h5>Command Modes
<pre>Twamp client control-connection session-request mode</pre>

<h5>Example
<pre>N1(twamp-client-session-request)# sender-udp-port 10000
N1(twamp-client-session-request)# no sender-udp-port</pre>

<h3>1.3.3.7.3 reflector-ip command
<h5>reflector-ip
<pre>Set reflector ipv4 address for twamp test. The IP address belonging to the remote Session-Reflector device to which the TWAMP-Test session will be initiated. This value will be used to populate the receiver address field of the Request-TW-Session message</pre>

<pre>reflector-ip A.B.C.D
no reflector-ip</pre>

<h5>Syntax Description
<pre>A.B.C.D
	Reflector ipv4 address</pre>

<h5>Default
<pre>None</pre>

<h5>Command Modes
<pre>Twamp client control-connection session-request mode</pre>

<h5>Example
<pre>N1(twamp-client-session-request)# reflector-ip 1.1.1.2
N1(twamp-client-session-request)# no reflector-ip</pre>

<h3>1.3.3.7.4 reflector-udp-port command
<h5>reflector-udp-port
<pre>Set reflector udp port for twamp test. This parameter defines the UDP port number that will be used by the Session-Reflector for this TWAMP-Test session. The number is restricted to the dynamic port range and is to be placed in the Receiver Port field of the Request-TW-Session message. If this value is not set, the device SHALL use the same port number as defined in the server-tcp-port parameter of this test-session-request’s parent twamp/client/ctrl-connection.</pre>

<pre>reflector-udp-port [100-65535]
no reflector-udp-port</pre>

<h5>Syntax Description
<pre>[100-65535]
	Reflector udp port</pre>

<h5>Default
<pre>None</pre>

<h5>Command Modes
<pre>Twamp client control-connection session-request mode</pre>

<h5>Example
<pre>N1(twamp-client-session-request)# reflector-udp-port 10000
N1(twamp-client-session-request)# no reflector-udp-port</pre>

<h3>1.3.3.7.5 timeout command
<h5>timeout
<pre>Set timeout for twamp test.  The length of time (in seconds) that the Session-Reflector should continue to respond to packets belonging to this TWAMP-Test session after a Stop-Sessions TWAMP-Control message has been received (RFC 5357, Section 3.8). This value will be placed in the Timeout field of the Request-TW-Session message.</pre>

<pre>timeout [0-100]
no timeout</pre>

<h5>Syntax Description
<pre>[0-100]
	Timeout seconds</pre>

<h5>Default
<pre>Default is "2" seconds</pre>

<h5>Command Modes
<pre>Twamp client control-connection session-request mode</pre>

<h5>Example
<pre>N1(twamp-client-session-request)# timeout 10
N1(twamp-client-session-request)# no timeout</pre>

<h3>1.3.3.7.6 test-packet-dscp command
<h5>test-packet-dscp
<pre>Set dscp value for twamp test. The DSCP value to be placed in the IP header of TWAMP-Test packets generated by the Session-Sender, and in the UDP header of the TWAMP-Test response packets generated by the Session-Reflector for this test session. This value will be placed in the Type-P Descriptor field of the Request-TW-Session message (RFC 5357).</pre>

<pre>test-packet-dscp [0-255]
no test-packet-dscp</pre>

<h5>Syntax Description
<pre>[0-255]
	Test packet’s dscp value.</pre>

<h5>Default
<pre>Default is "0"</pre>

<h5>Command Modes
<pre>Twamp client control-connection session-request mode</pre>

<h5>Example
<pre>N1(twamp-client-session-request)# test-packet-dscp 10
N1(twamp-client-session-request)# no test-packet-dscp</pre>

<h3>1.3.3.7.7 repeat command
<h5>repeat
<pre>Set repeat value for twamp test. This value determines if the TWAMP-Test session must be repeated. When a test session has completed, the repeat parameter is checked. The value of 0 indicates that the session MUST NOT be repeated. If the value is 1 through 4,294,967,294 then the test session SHALL be repeated using the information in repeat-interval parameter, and the parent TWAMP-Control connection for this test session is restarted to negotiate a new instance of this TWAMP-Test session. The implementation MUST decrement the value of repeat after determining a repeated session is expected. The value of 4,294,967,295 indicates that the test session SHALL be repeated *forever* using the information in repeat-interval parameter, and SHALL NOT decrement the value.</pre>

<pre>repeat [0-4294967294]
no repeat</pre>

<h5>Syntax Description
<pre>[0-4294967294]
	Repeat number</pre>

<h5>Default
<pre>Default is "0"</pre>

<h5>Command Modes
<pre>Twamp client control-connection session-request mode</pre>

<h5>Example
<pre>N1(twamp-client-session-request)# repeat 10
N1(twamp-client-session-request)# no repeat</pre>

<h3>1.3.3.7.8 repeat-interval command
<h5>repeat-interval
<pre>Set repeat-interval value for twamp test. This parameter determines the timing of repeated test sessions when repeat is more than 0. When the value of repeat-interval is 0, the negotiation of a new test session SHALL begin immediately after the previous test session completes. Otherwise, the Control-Client will wait for the number of minutes specified in the repeat-interval parameter before negotiating the new instance of this TWAMP-Test session.</pre>

<pre>repeat-interval [0-4294967294]
no repeat-interval</pre>

<h5>Syntax Description
<pre>[0-4294967294]
	Repeat-interval time (minutes)</pre>

<h5>Default
<pre>Default is "0"</pre>

<h5>Command Modes
<pre>Twamp client control-connection session-request mode</pre>

<h5>Example
<pre>N1(twamp-client-session-request)# repeat-interval 10
N1(twamp-client-session-request)# no repeat-interval</pre>


<h3>1.3.4 monitor command
<h5>monitor
<pre>Enter “twamp client monitor” mode. </pre>

<pre>(no) monitor</pre>

<h5>Syntax Description
<pre>None</pre>

<h5>Default
<pre>None</pre>

<h5>Command Modes
<pre>Twamp client mode</pre>

<h5>Example
<pre>N1(twamp-client)# monitor
N1(twamp-client)# no monitor</pre>


<h3>1.3.4.1 max-connection command
<h5>max-connection
<pre>Set the number of max clients to be connected</pre>

<pre>max-connection [1-10]
no max-connection</pre>

<h5>Syntax Description
<pre>[1-10]
	Number of max clients</pre>

<h5>Default
<pre>Default is "5"</pre>

<h5>Command Modes
<pre>Twamp client monitor mode</pre>

<h5>Example
<pre>N1(twamp-client-monitor)# max-connection 6
N1(twamp-server-control-connection)# no max-connection</pre>

<h3>1.3.4.2 listen-tcp-port command
<h5>listen-tcp-port
<pre>Set tcp listen port number for monitor clients to be connect</pre>

<pre>listen-tcp-port [100-65535]
no listen-tcp-port</pre>

<h5>Syntax Description
<pre>[100-65535]
	Tcp-port number</pre>

<h5>Default
<pre>Default is "22222"</pre>

<h5>Command Modes
<pre>Twamp client monitor mode</pre>

<h5>Example
<pre>N1(twamp-client-monitor)# listen-tcp-port 22222
N1(twamp-server-control-connection)# no listen-tcp-port</pre>

<h3>1.3.4.3 client-ip command
<h5>client-ip
<pre>Set monitor client ip to be allowed</pre>

<pre>client-ip A.B.C.D
no client-ip</pre>

<h5>Syntax Description
<pre>A.B.C.D
	Ipv4 address</pre>

<h5>Default
<pre>None</pre>

<h5>Command Modes
<pre>Twamp client monitor mode</pre>

<h5>Example
<pre>N1(twamp-client-monitor)# client-ip 1.2.3.4
N1(twamp-server-control-connection)# no client-ip</pre>


<h3>1.4 twamp sender command
<h5>twamp sender
<pre>Enter the TWAMP sender configuration mode.</pre>

<pre>(no) twamp sender</pre>

<h5>Syntax Description
<pre>None</pre>

<h5>Default
<pre>Default is “no twamp sender”.</pre>

<h5>Command Modes
<pre>System Configuration Mode</pre>

<h5>Example
<pre>N1(config)# twamp sender
N1(config)# no twamp sender</pre>


<h3>1.4.1 test-session command
<h5>test-session
<pre>Enter “twamp sender test-session” mode. </pre>

<pre>(no) test-session WORD</pre>

<h5>Syntax Description
<pre>WORD
	String value for test-session</pre>

<h5>Default
<pre>None</pre>

<h5>Command Modes
<pre>Twamp sender mode</pre>

<h5>Example
<pre>N1(twamp-sender)# test-session TEST-01
N1(twamp-sender)# no test-session TEST-01</pre>

<h3>1.4.1.1 control-connection-name command
<h5>control-connection-name
<pre>Specify control-connection-name. The name of the parent TWAMP-Control connection that is responsible for negotiating this TWAMP-Test session.</pre>

<pre>(no) control-connection-name WORD</pre>

<h5>Syntax Description
<pre>WORD
	String value for control-connection.</pre>

<h5>Default
<pre>None</pre>

<h5>Command Modes
<pre>Twamp sender test-session mode</pre>

<h5>Example
<pre>N1(twamp-sender- session-request)# control-connection-name CONN-01
N1(twamp-sender- session-request)# no control-connection-name CONN-01</pre>


<h3>1.4.1.2 number-of-packet command
<h5>number-of-packet
<pre>Specify number of packet. The overall number of TWAMP-Test (UDP) packets to be transmitted by the Session-Sender for this test session.</pre>

<pre>number-of-packet ]1-4294967295]
no number-of-packet</pre>

<h5>Syntax Description
<pre>[1-4294967295]
	Number of packet</pre>

<h5>Default
<pre>Default is "1"</pre>

<h5>Command Modes
<pre>Twamp sender test-session mode</pre>

<h5>Example
<pre>N1(twamp-sender- session-request)# number-of-packet 10
N1(twamp-sender- session-request)# no number-of-packet</pre>


<h3>1.4.1.3 interval command
<h5>interval
<pre>Interval time between each test packets.</pre>

<pre>interval [1-4294967295] sec | msec
no interval</pre>

<h5>Syntax Description
<pre>[1-4294967295]
	Interval time between test packets</pre>

<h5>Default
<pre>Default is "1" second</pre>

<h5>Command Modes
<pre>Twamp sender test-session mode</pre>

<h5>Example
<pre>N1(twamp-sender-session-request)# interval 1 sec
N1(twamp-sender-session-request)# no interval</pre>

<h2>2 Exec Command

<h3>2.1 show twamp light command
<h3>2.1.1 show twamp light status command
<h5>show service twamp light status
<pre>Show twamp light parameters.</pre>

<pre>show twamp light status</pre>

<h5>Syntax Description
<pre>None</pre>

<h5>Default
<pre>None</pre>

<h5>Command Modes
<pre>System Execution Mode</pre>

<h5>Example
<pre>N1(exec)# show twamp light status</pre>

<h3>2.2. show twamp server command
<h3>2.2.1 show twamp server status command

<h5>show service twamp server status
<pre>Show twamp parameters.</pre>

<pre>show twamp server status
show twamp server</pre>

<h5>Syntax Description
<pre>None</pre>

<h5>Default
<pre>None</pre>

<h5>Command Modes
<pre>System Execution Mode</pre>

<h5>Example
<pre>N2(exec)#show twamp server status 
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
  test inactivity timeout : 65 seconds</pre>


<h3>2.2.2 show twamp server sessions command
<h5>show twamp server session
<pre>Show all sessions of twamp connection</pre>

<pre>show twamp server session</pre>

<h5>Syntax Description
<pre>None</pre>

<h5>Default
<pre>None</pre>

<h5>Command Modes
<pre>System execution mode</pre>

<h5>Example
<pre>N1(exec)#show twamp server sessions
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
      receiver-ip/port : 1.1.1.2/30001</pre>


<h3>2.2.3 show twamp server session detail command
<h5>show twamp server session detail
<pre>Show all sessions’s detail information of twamp connections</pre>

<pre>show twamp server session detail</pre>

<h5>Syntax Description
<pre>None</pre>

<h5>Default
<pre>None</pre>

<h5>Command Modes
<pre>System execution mode</pre>

<h5>Example
<pre>N1(exec)#show twamp server sessions detail
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
      test-hmac-sha1-session-key : fa534b41f3fe6003208df8388c8d2fdfbb05de16aaaa276e767ce571be8d2eca</pre>

<h3>2.3 show twamp client command
<h5>2.3.1 show twamp client status command
<pre>show service twamp server status
Show twamp client parameters.</pre>

<pre>show twamp client
show twamp client status</pre>

<h5>Syntax Description
<pre>None</pre>

<h5>Default
<pre>None</pre>

<h5>Command Modes
<pre>System Execution Mode</pre>

<h5>Example
<pre>N1(exec)#show twamp client
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
      reflector IP : 1.1.1.12</pre>

<h3>2.3.2 show twamp client session command
<h5>show twamp client session
<pre>Show all information of twamp client sessions</pre>

<pre>show twamp client session</pre>

<h5>Syntax Description
<pre>None</pre>

<h5>Default
<pre>None</pre>

<h5>Command Modes
<pre>System execution mode</pre>

<h5>Example
<pre>N1(exec)#show twamp client session 
[client ip/port 192.168.122.101/48470 server ip/port 192.168.122.102/862]
  name : CONN-N2
  status : active
  mode : Authenticated
  key-id : key01
  number of test session : 1
    SID : 17e43a200d0f4ea8668f43a2e43344a1
      mode : Authenticated
      sender-ip/port : 1.1.1.11/20000
      receiver-ip/port : 1.1.1.12/20000</pre>

<h3>2.3.3 show twamp client session WORD command
<h5>show twamp client session WORD
<pre>Show detail informations of specific twamp session.</pre>

<pre>show twamp client session WORD</pre>

<h5>Syntax Description
<pre>WORD
	Twamp test-session name</pre>

<h5>Default
<pre>None</pre>

<h5>Command Modes
<pre>System execution mode</pre>

<h5>Example
<pre>N1(exec)#show twamp client session CONN-N2
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
      test-hmac-sha1-session-key : 3c18a35a111f2918a69080de5adf22a16d90a54d37df332afd99d6c6a65d0ae9</pre>

<h3>2.4 show twamp sender command
<h3>2.4.1 show twamp sender status command
<h5>show service twamp sender status
<pre>Show twamp sender parameters.</pre>

<pre>show twamp sender
show twamp sender status</pre>

<h5>Syntax Description
<pre>None</pre>

<h5>Default
<pre>None</pre>

<h5>Command Modes
<pre>System Execution Mode</pre>

<h5>Example
<pre>N1(exec)#show twamp sender 
twamp sender
  test-session TEST-N2
    control-connection-name is CONN-N2
    fill-mode : zero
    number-of-packet : 1000000
    interval : 1 seconds</pre>

<h3>2.4.2 show twamp sender session command
<h5>show service twamp session
<pre>Show all session’s information of twamp sender</pre>

<pre>show twamp sender session</pre>

<h5>Syntax Description
<pre>None</pre>

<h5>Default
<pre>None</pre>

<h5>Command Modes
<pre>System Execution Mode</pre>

<h5>Example
<pre>N1(exec)#show twamp sender session 
twamp sender
  test-session TEST-N2
    control-connection-name is CONN-N2
  test-session TEST-N3
    control-connection-name is CONN-N3
  test-session TEST-N4
control-connection-name is CONN-N4</pre>

<h3>2.4.3 show twamp sender session WORD command
<h5>show service twamp session WORD
<pre>Show detail information of specific twamp session</pre>

<pre>show twamp sender session WORD</pre>

<h5>Syntax Description
<pre>WROD
	Twamp test-session name</pre>
<h5>Default
<pre>None</pre>

<h5>Command Modes
<pre>System Execution Mode</pre>

<h5>Example
<pre>N1(exec)#show twamp sender session TEST-N2
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
      max variation : 0 sec 1761 usec</pre>

<h3>2.5 twping command
<h5>twping A.B.C.D
<pre>A.B.C.D : Reflector ipv4 address.</pre>

<h5>twping A.B.C.D count [1-100]
<pre>A.B.C.D 	: Reflector ipv4 address.
count 	: number of test packet.</pre>

<h5>twping A.B.C.D count [1-100] reflector-port [100-65535]
<pre>A.B.C.D 	: Reflector ipv4 address.
count 	: number of test packet.
reflector-port	: upd port of reflector</pre>

<h5>twping A.B.C.D mode (unauthenticated|authenticated|encrypted|mixed) key-id WORD secret-key WORD
<pre>A.B.C.D 	: Reflector ipv4 address.
mode 	: unauthenticated|authenticated|encrypted|mixed
key-id	: string value of key-id
secret-key	: string value of passphrase</pre>

<h5>twping A.B.C.D server-tcp-port [100-65535] mode (unauthenticated|authenticated|encrypted|mixed) key-id WORD secret-key WORD
<pre>A.B.C.D 	: Reflector ipv4 address.
server-tcp-port	: tcp port of server
mode 	: unauthenticated|authenticated|encrypted|mixed
key-id	: string value of key-id
secret-key	: string value of passphrase</pre>

<h5>twping A.B.C.D count [1-100] mode (unauthenticated|authenticated|encrypted|mixed) key-id WORD secret-key WORD
<pre>A.B.C.D 	: Reflector ipv4 address.
count 	: number of test packet.
mode 	: unauthenticated|authenticated|encrypted|mixed
key-id	: string value of key-id
secret-key	: string value of passphrase</pre>

<h5>twping A.B.C.D count [1-100] server-tcp-port [100-65535] mode (unauthenticated|authenticated|encrypted|mixed) key-id WORD secret-key WORD
<pre>A.B.C.D 	: Reflector ipv4 address.
count 	: number of test packet.
server-tcp-port	: tcp port of server
mode 	: unauthenticated|authenticated|encrypted|mixed
key-id	: string value of key-id
secret-key	: string value of passphrase</pre>

<h5>twping A.B.C.D count [1-100] session-count [2-100] mode (unauthenticated|authenticated|encrypted|mixed) key-id WORD secret-key WORD
<pre>A.B.C.D 	: Reflector ipv4 address.
count 	: number of test packet.
session-count	: number of test sessions
mode 	: unauthenticated|authenticated|encrypted|mixed
key-id	: string value of key-id
secret-key	: string value of passphrase</pre>

<h5>twping A.B.C.D count [1-100] session-count [2-100] server-tcp-port [100-65535] mode (unauthenticated|authenticated|encrypted|mixed) key-id WORD secret-key WORD
<pre>A.B.C.D 	: Reflector ipv4 address.
count 	: number of test packet.
session-count	: number of test sessions
server-tcp-port	: tcp port of server
mode 	: unauthenticated|authenticated|encrypted|mixed
key-id	: string value of key-id
secret-key	: string value of passphrase</pre>

<h5>Command Modes
<pre>System Execution Mode</pre>

<h5>Example

<h5>Twping with configuration (Background process)
<h5>twping start sender-test-session WORD
<pre>twping start sender-test-session TEST-N2</pre>

<h5>Twping with TWAMP Light Server
<h5>twping A.B.C.D
<pre>N1(exec)# twping 1.1.1.12</pre>

<h5>twping A.B.C.D count [1-100]
<pre>N1(exec)# twping 1.1.1.12 count 10</pre>

<h5>twping A.B.C.D reflector-port [100-65535]
<pre>N1(exec)# twping 1.1.1.12 reflector-port 863</pre>

<h5>twping A.B.C.D count [1-100] reflector-port [100-65535]
<pre>N1(exec)# twping 1.1.1.12 count 10 reflector-port 863</pre>

<h5>Twping with TWAMP Full Server
<h5>twping A.B.C.D mode (unauthenticated|authenticated|encrypted|mixed) key-id WORD secret-key WORD
<pre>N1(exec)# twping 1.1.1.12 mode unauthenticated key-id user01 secret-key password01
N1(exec)# twping 1.1.1.12 mode authenticated key-id user01 secret-key password01
N1(exec)# twping 1.1.1.12 mode encrypted key-id user01 secret-key password01
N1(exec)# twping 1.1.1.12 mode mixed key-id user01 secret-key password01</pre>

<h5>twping A.B.C.D count [2-100] mode (unauthenticated|authenticated|encrypted|mixed) key-id WORD secret-key WORD
<pre>N1(exec)# twping 1.1.1.12 count 5 mode unauthenticated key-id user01 secret-key password01
N1(exec)# twping 1.1.1.12 count 5 mode authenticated key-id user01 secret-key password01
N1(exec)# twping 1.1.1.12 count 5 mode encrypted key-id user01 secret-key password01
N1(exec)# twping 1.1.1.12 count 5 mode mixed key-id user01 secret-key password01</pre>

<h5>twping A.B.C.D count [2-100] session-count [2-100] mode (unauthenticated|authenticated|encrypted|mixed) key-id WORD secret-key WORD
<pre>N1(exec)# twping 1.1.1.12 count 5 session-count 5 mode unauthenticated key-id user01 secret-key password01
N1(exec)# twping 1.1.1.12 count 5 session-count 5 mode authenticated key-id user01 secret-key password01
N1(exec)# twping 1.1.1.12 count 5 session-count 5 mode encrypted key-id user01 secret-key password01
N1(exec)# twping 1.1.1.12 count 5 session-count 5 mode mixed key-id user01 secret-key password01</pre>

<h5>twping A.B.C.D server-tcp-port [100-65535] mode (unauthenticated|authenticated|encrypted|mixed) key-id WORD secret-key WORD
<pre>N1(exec)# twping 1.1.1.12 server-port 863 mode unauthenticated user user01 password password01
N1(exec)# twping 1.1.1.12 server-port 863 mode authenticated user user01 password password01
N1(exec)# twping 1.1.1.12 server-port 863 mode encrypted user user01 password password01
N1(exec)# twping 1.1.1.12 server-port 863 mode mixed user user01 password password01</pre>

<h5>twping A.B.C.D count [1-100] server-tcp-port [100-65535] mode (unauthenticated|authenticated|encrypted|mixed) key-id WORD secret-key WORD
<pre>N1(exec)# twping 1.1.1.12 count 5 server-port 863 mode unauthenticated user user01 password password01
N1(exec)# twping 1.1.1.12 count 5 server-port 863 mode authenticated user user01 password password01
N1(exec)# twping 1.1.1.12 count 5 server-port 863 mode encrypted user user01 password password01
N1(exec)# twping 1.1.1.12 count 5 server-port 863 mode mixed user user01 password password01</pre>

<h5>twping A.B.C.D count [1-100] session-count [2-100] server-tcp-port [100-65535] mode (unauthenticated|authenticated|encrypted|mixed) key-id WORD secret-key WORD
<pre>N1(exec)# twping 1.1.1.12 count 5 session-count 5 server-port 863 mode unauthenticated user user01 password password01
N1(exec)# twping 1.1.1.12 count 5 session-count 5 server-port 863 mode authenticated user user01 password password01
N1(exec)# twping 1.1.1.12 count 5 session-count 5 server-port 863 mode encrypted user user01 password password01
N1(exec)# twping 1.1.1.12 count 5 session-count 5 server-port 863 mode mixed user user01 password password01</pre>
