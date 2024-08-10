# rtbh-helper
Script to allow for RTBH routes to be injected into the network for your ASN, or your customer

# Requirements

- Know what you're doing with RTBH :-)
- Have FRR setup and configured on the local machine, with BGP sessions and policy to the right devices in your network
- Have BGP policies to protect yourself from doing something silly with this script (e.g. trying to RTBH something you shouldn't and leaking that to your upstreams)
- BGP policies and communities for originated and customer RTBH
- Optionally, BGP policies and communities for local RTBH (e.g. blackhole inside my network) and global RTBH (e.g. send blackhole communities to transits/peers)

# Caveats

- This script does no checking whatsoever to see if you're allowed to advertise the prefix/asn pair - we expect your upstream routers to be applying the right policies and filters
- If the FRR instance is restarted, the script won't remember what was previously advertised for blackholing - you'll need to wrap this helper with something else todo that for you

# How to use
