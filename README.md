# rtbh-helper
Script to allow for RTBH routes to be injected into the network for your ASN, or your customer

# Requirements

- FRR setup and configured on the local machine, with BGP sessions to the right devices in your network
- BGP policies for originated and customer RTBH
- Optionally, BGP policies and communities for local RTBH (e.g. blackhole inside my network) and global RTBH (e.g. send blackhole communities to transits/peers)
