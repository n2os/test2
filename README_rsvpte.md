<h1>RSVP-TE Command Guide</h1>

<h2>Command Summary</h2>
<h3>Configuration Mode Command</h2>
<h4>router rsvp Node</h4>
<pre>
(no)router rsvp 
(no)refresh
    (no)router-alert
    encap-num <1-350>
    (no)confirm
    (no)lsr-id A.B.C.D
    (no)refresh-interval <1-65535>
    (no)refresh-multiplier <1-65535>
    (no)srefresh
    (no)srefresh-interval <1-65535>
    (no)msgack-interval <1-65535>
    (no)msgack-retry-multiplier <1-65535>
    (no)hello-interval <1-65535>
    (no)hello-multiplier <1-65535>
    (no)hello-receipt
    (no)explicit-null
    (no)loop-detection</pre>
        
<h4>rsvp path Node</h4>
<pre>
(no)rsvp path PATHNAME
	(no)A.B.C.D
	(no)A.B.C.D (strict|loose)</pre>
	
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
	(no)enable-rsvp
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
