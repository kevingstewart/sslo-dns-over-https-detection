# SSL Orchestrator DNS-over-HTTPS Detection
Set of iRule tools to add DoH detection to SSL Orchestrator

## Version support
These iRules work on all modern versions of BIG-IP (14.1+) and SSL Orchestrator (5.0+)

Based on RFC8484, DNS-over-HTTPS (DoH) is a method of securely conveying DNS requests/responses over encrypted HTTPS. While DoH is intended to provide additional privacy (i.e. DNS traffic is not protected from eavesdropping), it can have other serious implications as it also potentially masks malware command-and-control. In the absence of running a local DoH-capable DNS resolver, detection of DoH traffic minimally requires decryption and inspection. This repository provides a set of iRules that can be attached to an SSL Orchestrator configuration to provide the following DoH controls:

- **DoH Detection and Blocking**: This simply identifies any DoH request traffic, in any of the three DoH formats (Wireframe GET/POST and JSON) and sends a reject. A DoH-cable browser that receives reject on DoH request will revert to normal DNS.

- **DoH Detection and Logging**: This identifies DoH request traffic, and can:
  - Parse the query name and type (A, AAAA, TXT, etc.) for local and remote high-speed logging
  - Enable a DoH blackhole response for A, AAAA and TXT requests based on a URL category match (of the requested name)

------------------------------

## Installation
Installation is as simple as adding the respective iRule to an SSL Orchestrator topology. 

  - Under Local Traffic -> iRules in the BIG-IP UI, import the required iRule.
  - In the SSL Orchestrator UI, under the Interception Rules tab, click on the interception rule to edit (typically ending with "-in-t"), and at the bottom of this configuration page, add the iRule and then (re)deploy.
  - If using the DoH detection and logging iRule, additional configuration is required (see below).

## Configuration
Configuration in the DoH detection and logging iRule is performed through a set of static variables at the top of the rule:

  - **static::LOCAL_LOG**:

  - **static::HSL**:

  - **static::URLDB_LICENSED**:

  - **static::BLACKHOLE_URLS**:
  
  - **static::BLACKHOLE_RTYPE_A**:
  
  - **static::BLACKHOLE_RTYPE_AAAA**:
  
  - **static::BLACKHOLE_RTYPE_TXT**:
  
  - **static::dns_codes**:
  
  
  
