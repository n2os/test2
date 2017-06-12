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
<h2>Command Detail</h2>
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
