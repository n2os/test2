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
  (no)bfd A.B.C.D A.B.C.D
  (no)bfd A.B.C.D <1001-65535> A.B.C.D <1001-65535>
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

<h4>bfd monitor server</h4>
Set Ipv4 address and UDP port number of monitoring server.
<pre>
  (no)bfd montor server A.B.C.D port <1001-65535>
</pre>

<h5>Syntax Description</h5>
<pre>
A.B.C.D
	Monitor server’s Ipv4 Address.
<1001 – 65535>
  Monitor server’s UDP Port number.
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
N1(config)#  bfd monitor server 192.168.2.200 port 1005
</pre>

-----------------------------

<h4>bfd monitor client</h4>

<pre>
  (no)bfd montor client A.B.C.D   Client ipv4 address (e.g. 1.2.3.4)
</pre>

<h4>bfd session</h4>
<pre>
  (no)bfd A.B.C.D A.B.C.D
  (no)bfd A.B.C.D <1001-65535> A.B.C.D <1001-65535>
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
