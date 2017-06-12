<h1>RSVP-TE Command Guide</h1>

<h2>Command Summary</h2>
<h3>Configuration Mode Command</h2>
<h4>router rsvp Node</h4>
<pre>
(no)router rsvp 			set rsvpte global configuration
	(no)refresh			set refresh enable mode
	(no)router-alert		enable rsvpte router-alert option
	encap-num <1-350>		set encap number per summary refresh
	(no)confirm			enable rsvpte confirm object at egress
	(no)lsr-id A.B.C.D		set rsvpte label-switch-router identifier
	(no)refresh-interval <1-65535>	set rsvpte refresh interval[sec]
	(no)refresh-multiplier <1-65535> set rsvpte refresh multiplier
	(no)srefresh			enable rsvpte summary refresh
	(no)srefresh-interval <1-65535>	set summary refresh interval[sec]
	(no)msgack-interval <1-65535>	set rsvpte ack message interval[secs]
	(no)msgack-retry-multiplier <1-65535> set rsvpte ack message retry multiplier
	(no)hello-interval <1-65535>	set rsvpte hello interval[secs]
	(no)hello-multiplier <1-65535>	set rsvpte hello multiplier
	(no)hello-receipt		enable rsvpte hello function
	(no)explicit-null		enable rsvpte explicit null
	(no)loop-detection		enable rsvpte loop-detection function
</pre>
        
<h4>rsvp path Node</h4>
<pre>
(no)rsvp path PATHNAME			create rsvpte path info
	(no)A.B.C.D			add hop-address to path
	(no)A.B.C.D (strict|loose)	add hop-address to path
</pre>
	
<h4>rsvp trunk Node</h4>
<pre>
(no)rsvp trunk TRUNKNAME		create rsvpte trunk info
no rsvp trunk all
	(no)primary PATH_NAME		add rsvpte primary path info to trunk
	(no)secondary PATH_NAME		add rsvpte secondary path info to trunk
	(no)from A.B.C.D 		add rsvpte ingress address to trunk
	(no)to A.B.C.D			add rsvpte egress address to trunk
	(no)uni-srctna A.B.C.D          UNI
	(no)uni-dsttna A.B.C.D          UNI
	(no)uni-diversity <1-65535>     UNI
	(no)uni-service-level <1-65535> UNI
	(no)filter (fixed-filter|shared-explicit) add rsvpte filter-style to trunk
	(no)bandwidth <1-65535>		add rsvpte request bandwidth to trunk
	(no)hop-limit <1-255>		add rsvpte hop-limit to trunk
	(no)cspf			use rsvpte cspf-explicit-route to trunk
	(no)hold-priority <0-7>		add hold-priority to trunk
	(no)setup-priority <0-7>	add setup-priority to trunk
	(no)record-route		set record-route use to trunk
	(no)label-record		set label-record use to trunk
	(no)diffserv-elsp phb-id PHB-ID exp <0-7> set diffserv e-lsp to trunk
	(no)diffserv-llsp psc PSC-ID	setting diffserv l-lsp info to trunk
	(no)number <1-65536>		number of trunk that we want setup
	run				triggering rsvpte trunk</pre>

<h4>interface Node</h4>
<pre>
interface IF-NAME			
	(no)enable-rsvp			router interface configuration enable rsvp-te
	(no)enable-rsvp-integrity KEY_ID enable rsvp-te authentication
	(no)enable-rsvp-integrity KEY_ID (md5|hmac-md5) enable rsvp-te integrity usage
	(no)enable-rsvp-message-id	enable rsvp-te message-id usage
	(no)enable-rsvp-hello		enable rsvp-te hello on this interface
	(no)enable-rsvp-unic		UNI-C
	(no)enable-rsvp-unin		UNI-N</pre>

<h4>debug command</h4>
<pre>
debug rsvp
(no)debug rsvp event
(no)debug rsvp hexdump
(no)debug rsvp packet
(no)debug rsvp packet detail
(no)debug rsvp psb-rsb-count
// debug uni
(no)debug rsvp uni if-msg</pre>

<h3>Configuration Mode Command</h2>

<h4>show command</h4>
<pre>
show rsvp	
show rsvp version
show rsvp debug
show rsvp path
show rsvp path PATH_NAME
show rsvp trunk
show rsvp trunk TRUNK_NAME
show rsvp session
show rsvp session summary
show rsvp session detail
show rsvp psb-rsb
show rsvp interface
show rsvp interface IF_NAME
show rsvp neighbor status
show rsvp statistics
show rsvp memory-usage</pre>

<h4>clear command</h4>
<pre>
clear rsvp statistics
clear rsvp session TRUNK_NAME
clear rsvp session all

// uni clear
clear rsvp uni session lsp-id <1-65535> tunnel-id <1-65535> src-addr A.B.C.D dst-addr A.B.C.D
clear rsvp uni session all
</pre>

==================================================================================
<h1>Command Detail</h1>
<h2>1. Configuration Mode Command</h2>

<h3>1.1 router rsvp</h3>
<h5>router rsvp</h5>
<pre>Set rsvpte global configuration.</pre>
<pre>(no) router rsvp</pre>

<h5> Syntax Description</h5>
<pre>None </pre>

<h5> Default</h5>
<pre>Default is “no router rsvp”. </pre>

<h5> Command Modes</h5>
<pre>System Configuration Mode </pre>

<h5> Example</h5>
<pre>N1(config)# router rsvp
N1(config)# no router rsvp</pre>

<h3>1.1.1 refresh</h3>
<h5>refresh</h5>
<pre>Set refresh enable mode.</pre>
<pre>(no) refresh</pre>

<h5> Syntax Description</h5>
<pre>None</pre>

<h5> Default</h5>
<pre>Default is “refresh”. </pre>

<h5> Command Modes</h5>
<pre>Router Rsvp Mode </pre>

<h5> Example</h5>
<pre>N1(config-router)# refresh
N1(config-router)# no refresh</pre>

<h3>1.1.2 router-alert</h3>
<h5>router-alert</h5>
<pre>enable rsvpte router-alert option.</pre>
<pre>(no) router-alert</pre>

<h5> Syntax Description</h5>
<pre>None</pre>

<h5> Default</h5>
<pre>Default is “router-alert”. </pre>

<h5> Command Modes</h5>
<pre>Router Rsvp Mode </pre>

<h5> Example</h5>
<pre>N1(config-router)# router-alert
N1(config-router)# no router-alert</pre>

<h3>1.1.3 encap-num</h3>
<h5>encap-num</h5>
<pre>set encap number per summary refresh.</pre>
<pre>(no) encap-num <1-350></pre>

<h5> Syntax Description</h5>
<pre><1-350>
	Number per summary refresh</pre>

<h5> Default</h5>
<pre>Default is “350”. </pre>

<h5> Command Modes</h5>
<pre>Router Rsvp Mode </pre>

<h5> Example</h5>
<pre>N1(config-router)# encap-num 100
N1(config-router)# no encap-num</pre>

<h3>1.1.4 confirm</h3>
<h5>confirm</h5>
<pre>enable rsvpte confirm object at egress.</pre>
<pre>(no) confirm</pre>

<h5> Syntax Description</h5>
<pre>None</pre>

<h5> Default</h5>
<pre>Default is “no confirm”. </pre>

<h5> Command Modes</h5>
<pre>Router Rsvp Mode </pre>

<h5> Example</h5>
<pre>N1(config-router)# confirm
N1(config-router)# no confirm</pre>

<h3>1.1.5 lsr-id</h3>
<h5>lsr-id</h5>
<pre>set rsvpte label-switch-router identifier.</pre>
<pre>(no) lsr-id A.B.C.D</pre>

<h5> Syntax Description</h5>
<pre>A.B.C.D
	LSR Identifier</pre>

<h5> Default</h5>
<pre>Default is “no lsr-id”. </pre>

<h5> Command Modes</h5>
<pre>Router Rsvp Mode </pre>

<h5> Example</h5>
<pre>N1(config-router)# lsr-id 1.1.1.11
N1(config-router)# no lsr-id</pre>


<h3>1.1.6 refresh-interval</h3>
<h5>refresh-interval</h5>
<pre>set rsvpte refresh interval[sec].</pre>
<pre>(no)refresh-interval <1-65535></pre>

<h5> Syntax Description</h5>
<pre><1-65535>
	Refresh interval(sec)</pre>

<h5> Default</h5>
<pre>Default is “30 sec”. </pre>

<h5> Command Modes</h5>
<pre>Router Rsvp Mode </pre>

<h5> Example</h5>
<pre>N1(config-router)# refresh-interval 10
N1(config-router)# no refresh-interval</pre>


<h3>1.1.7 refresh-multiplier</h3>
<h5>refresh-multiplier</h5>
<pre>set rsvpte refresh multiplier.</pre>
<pre>(no) refresh-multiplier <1-65535></pre>

<h5> Syntax Description</h5>
<pre><1-65535>
	Refresh multiplier</pre>

<h5> Default</h5>
<pre>Default is “3”. </pre>

<h5> Command Modes</h5>
<pre>Router Rsvp Mode </pre>

<h5> Example</h5>
<pre>N1(config-router)# refresh-multiplier 10
N1(config-router)# no refresh-multiplier</pre>


<h3>1.1.8 srefresh</h3>
<h5>srefresh</h5>
<pre>enable rsvpte summary refresh.</pre>
<pre>(no) srefresh<1-65535></pre>

<h5> Syntax Description</h5>
<pre>None</pre>

<h5> Default</h5>
<pre>Default is “no srefresh”. </pre>

<h5> Command Modes</h5>
<pre>Router Rsvp Mode </pre>

<h5> Example</h5>
<pre>N1(config-router)# srefresh
N1(config-router)# no srefresh</pre>


<h3>1.1.9 srefresh-interval</h3>
<h5>srefresh-interval</h5>
<pre>set summary refresh interval[sec].</pre>
<pre>(no)srefresh-interval <1-65535></pre>

<h5> Syntax Description</h5>
<pre><1-65535>
	Summary refresh interval[sec]</pre>

<h5> Default</h5>
<pre>Default is “3”. </pre>

<h5> Command Modes</h5>
<pre>Router Rsvp Mode </pre>

<h5> Example</h5>
<pre>N1(config-router)# srefresh-interval 10
N1(config-router)# no srefresh-interval</pre>


<h3>1.1.10 msgack-interval</h3>
<h5>msgack-interval</h5>
<pre>set rsvpte ack message interval[secs].</pre>
<pre>(no)msgack-interval <1-65535></pre>

<h5> Syntax Description</h5>
<pre><1-65535>
	Ack mesage interval[sec]</pre>

<h5> Default</h5>
<pre>Default is “1”. </pre>

<h5> Command Modes</h5>
<pre>Router Rsvp Mode </pre>

<h5> Example</h5>
<pre>N1(config-router)# msgack-interval 3
N1(config-router)# no msgack-interval</pre>


<h3>1.1.11 msgack-retry-multiplier</h3>
<h5>msgack-retry-multiplier</h5>
<pre>set rsvpte ack message retry multiplier.</pre>
<pre>(no)msgack-retry-multiplier <1-65535></pre>

<h5> Syntax Description</h5>
<pre><1-65535>
	Ack mesage multiplier</pre>

<h5> Default</h5>
<pre>Default is “3”. </pre>

<h5> Command Modes</h5>
<pre>Router Rsvp Mode </pre>

<h5> Example</h5>
<pre>N1(config-router)# msgack-retry-multiplier 10
N1(config-router)# no msgack-retry-multiplier</pre>


<h3>1.1.12 hello-interval</h3>
<h5>hello-interval</h5>
<pre>set rsvpte hello interval[secs].</pre>
<pre>(no) hello-interval <1-65535></pre>

<h5> Syntax Description</h5>
<pre><1-65535>
	Hello interval[secs]</pre>

<h5> Default</h5>
<pre>Default is “3”. </pre>

<h5> Command Modes</h5>
<pre>Router Rsvp Mode </pre>

<h5> Example</h5>
<pre>N1(config-router)# hello-interval 1
N1(config-router)# no hello-interval</pre>


<h3>1.1.13 hello-multiplier</h3>
<h5>hello-multiplier</h5>
<pre>set rsvpte hello multiplier.</pre>
<pre>(no) hello-multiplier <1-65535></pre>

<h5> Syntax Description</h5>
<pre><1-65535>
	Hello multiplier</pre>

<h5> Default</h5>
<pre>Default is “3”. </pre>

<h5> Command Modes</h5>
<pre>Router Rsvp Mode </pre>

<h5> Example</h5>
<pre>N1(config-router)# hello-multiplier 10
N1(config-router)# no hello-multiplier</pre>


<h3>1.1.14 hello-receipt</h3>
<h5>hello-receipt</h5>
<pre>enable rsvpte hello function.</pre>
<pre>(no) hello-receipt</pre>

<h5> Syntax Description</h5>
<pre>None</pre>

<h5> Default</h5>
<pre>Default is “hello-recipt”. </pre>

<h5> Command Modes</h5>
<pre>Router Rsvp Mode </pre>

<h5> Example</h5>
<pre>N1(config-router)# hello-receipt
N1(config-router)# no hello-receipt</pre>


<h3>1.1.15 explicit-null</h3>
<h5>explicit-null</h5>
<pre>enable rsvpte explicit null.</pre>
<pre>(no) explicit-null</pre>

<h5> Syntax Description</h5>
<pre>None</pre>

<h5> Default</h5>
<pre>Default is “no explicit-null”. </pre>

<h5> Command Modes</h5>
<pre>Router Rsvp Mode </pre>

<h5> Example</h5>
<pre>N1(config-router)# explicit-null
N1(config-router)# no explicit-null</pre>


<h3>1.1.16 loop-detection</h3>
<h5>loop-detection</h5>
<pre>enable rsvpte loop-detection function.</pre>
<pre>(no) loop-detection</pre>

<h5> Syntax Description</h5>
<pre>None</pre>

<h5> Default</h5>
<pre>Default is “no loop-detection”. </pre>

<h5> Command Modes</h5>
<pre>Router Rsvp Mode </pre>

<h5> Example</h5>
<pre>N1(config-router)# loop-detection
N1(config-router)# no loop-detection</pre>

==============================================================================

<h4>rsvp path Node</h4>
<pre>
(no)rsvp path PATHNAME			create rsvpte path info
	(no)A.B.C.D			add hop-address to path
	(no)A.B.C.D (strict|loose)	add hop-address to path
</pre>
	
<h4>rsvp trunk Node</h4>
<pre>
(no)rsvp trunk TRUNKNAME		create rsvpte trunk info
no rsvp trunk all
	(no)primary PATH_NAME		add rsvpte primary path info to trunk
	(no)secondary PATH_NAME		add rsvpte secondary path info to trunk
	(no)from A.B.C.D 		add rsvpte ingress address to trunk
	(no)to A.B.C.D			add rsvpte egress address to trunk
	(no)uni-srctna A.B.C.D          UNI
	(no)uni-dsttna A.B.C.D          UNI
	(no)uni-diversity <1-65535>     UNI
	(no)uni-service-level <1-65535> UNI
	(no)filter (fixed-filter|shared-explicit) add rsvpte filter-style to trunk
	(no)bandwidth <1-65535>		add rsvpte request bandwidth to trunk
	(no)hop-limit <1-255>		add rsvpte hop-limit to trunk
	(no)cspf			use rsvpte cspf-explicit-route to trunk
	(no)hold-priority <0-7>		add hold-priority to trunk
	(no)setup-priority <0-7>	add setup-priority to trunk
	(no)record-route		set record-route use to trunk
	(no)label-record		set label-record use to trunk
	(no)diffserv-elsp phb-id PHB-ID exp <0-7> set diffserv e-lsp to trunk
	(no)diffserv-llsp psc PSC-ID	setting diffserv l-lsp info to trunk
	(no)number <1-65536>		number of trunk that we want setup
	run				triggering rsvpte trunk</pre>

<h4>interface Node</h4>
<pre>
interface IF-NAME			
	(no)enable-rsvp			router interface configuration enable rsvp-te
	(no)enable-rsvp-integrity KEY_ID enable rsvp-te authentication
	(no)enable-rsvp-integrity KEY_ID (md5|hmac-md5) enable rsvp-te integrity usage
	(no)enable-rsvp-message-id	enable rsvp-te message-id usage
	(no)enable-rsvp-hello		enable rsvp-te hello on this interface
	(no)enable-rsvp-unic		UNI-C
	(no)enable-rsvp-unin		UNI-N</pre>

<h4>debug command</h4>
<pre>
debug rsvp
(no)debug rsvp event
(no)debug rsvp hexdump
(no)debug rsvp packet
(no)debug rsvp packet detail
(no)debug rsvp psb-rsb-count
// debug uni
(no)debug rsvp uni if-msg</pre>

<h3>Configuration Mode Command</h2>

<h4>show command</h4>
<pre>
show rsvp	
show rsvp version
show rsvp debug
show rsvp path
show rsvp path PATH_NAME
show rsvp trunk
show rsvp trunk TRUNK_NAME
show rsvp session
show rsvp session summary
show rsvp session detail
show rsvp psb-rsb
show rsvp interface
show rsvp interface IF_NAME
show rsvp neighbor status
show rsvp statistics
show rsvp memory-usage</pre>

<h4>clear command</h4>
<pre>
clear rsvp statistics
clear rsvp session TRUNK_NAME
clear rsvp session all

// uni clear
clear rsvp uni session lsp-id <1-65535> tunnel-id <1-65535> src-addr A.B.C.D dst-addr A.B.C.D
clear rsvp uni session all
</pre>
