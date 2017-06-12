<h1>RSVP-TE Command Guide</h1>

<h2>Command Summary</h2>
<h3>Configuration Mode Command</h2>
router rsvp Node
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
        
rsvp path Node
<pre>
(no)rsvp path PATHNAME
	(no)A.B.C.D
	(no)A.B.C.D (strict|loose)</pre>
	
	
// install node TRUNK
V(no)rsvp trunk TRUNKNAME		create rsvpte trunk info
Vno rsvp trunk TRUNKNAME
Vno rsvp trunk all
V	(no)primary PATH_NAME		add rsvpte primary path info to trunk
V	(no)secondary PATH_NAME		add rsvpte secondary path info to trunk
V	(no)from A.B.C.D 		add rsvpte ingress address to trunk
V	(no)to A.B.C.D			add rsvpte egress address to trunk
V	(no)uni-srctna A.B.C.D          UNI
V	(no)uni-dsttna A.B.C.D          UNI
V	(no)uni-diversity <1-65535>     UNI
V	(no)uni-service-level <1-65535> UNI
V	(no)filter (fixed-filter|shared-explicit) add rsvpte filter-style to trunk
V	(no)bandwidth <1-65535>		add rsvpte request bandwidth to trunk
V	(no)hop-limit <1-255>		add rsvpte hop-limit to trunk
V	(no)cspf			use rsvpte cspf-explicit-route to trunk
V	(no)hold-priority <0-7>		add hold-priority to trunk
V	(no)setup-priority <0-7>	add setup-priority to trunk
V	(no)record-route		set record-route use to trunk
V	(no)label-record		set label-record use to trunk
V	(no)diffserv-elsp phb-id PHB-ID exp <0-7> set diffserv e-lsp to trunk
V	(no)diffserv-llsp psc PSC-ID	setting diffserv l-lsp info to trunk
V	(no)number <1-65536>		number of trunk that we want setup
C	run				triggering rsvpte trunk

// interface command
Vinterface IF-NAME
V	(no)enable-rsvp
V	(no)enable-rsvp-integrity KEY_ID enable rsvp-te authentication
V	(no)enable-rsvp-integrity KEY_ID (md5|hmac-md5) enable rsvp-te integrity usage
V	(no)enable-rsvp-message-id	enable rsvp-te message-id usage
V	(no)enable-rsvp-hello		enable rsvp-te hello on this interface
V	(no)enable-rsvp-unic		UNI-C
V	(no)enable-rsvp-unin		UNI-N

// debug
debug rsvp
V(no)debug rsvp event
V(no)debug rsvp hexdump
V(no)debug rsvp packet
V(no)debug rsvp packet detail
V(no)debug rsvp psb-rsb-count

// debug uni
V(no)debug rsvp uni if-msg


// show rsvp
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
show rsvp memory-usage

// clear
clear rsvp statistics
clear rsvp session TRUNK_NAME
clear rsvp session all

// uni clear
clear rsvp uni session lsp-id <1-65535> tunnel-id <1-65535> src-addr A.B.C.D dst-addr A.B.C.D
clear rsvp uni session all
