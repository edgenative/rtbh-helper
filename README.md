# rtbh-helper
Script to allow for RTBH routes to be injected into the network for your ASN, or your customer.  I'm using this to locally rtbh bad actors hitting my web servers

# Requirements

- Know what you're doing with RTBH :-)
- Have FRR setup and configured on the local machine, with BGP sessions and policy to the right devices in your network (e.g. your core or your edge)
- Have BGP policies to protect yourself from doing something silly with this script (e.g. trying to RTBH something you shouldn't and leaking that to your upstreams)
- BGP policies and communities for originated and customer RTBH
- Optionally, BGP policies and communities for local RTBH (e.g. blackhole inside my network) and global RTBH (e.g. send blackhole communities to transits/peers)

# Caveats

- This script does no checking whatsoever to see if you're allowed to advertise the prefix/asn pair - we expect your upstream routers to be applying the right policies and filters to stop you doing crazy stuff
- If the FRR instance is restarted, the script won't remember what was previously advertised for blackholing - you'll need to wrap this helper with something else todo that for you

# How to use

- Install the rtbh script into your path somewhere.  Configure the values on lines 7 through 12 to include the right community values for your network.
  - Lines 7 and 8 are for global advertisement of RTBH routes.  Include the communities here that trigger your edge to advertise these prefixes to upstreams
  - Lines 11 and 12 are for the local versions of the above.  In my network, I use these to trigger RTBH across my own routers, but I don't leak these routes to upstreams.
- Run the script.  There are a few options here
  - rtbh --advertise x.x.x.x -- This will advertise the prefix, and add communities to send to your upstreams
  - rtbh --advertise x.x.x.x --asn 123 -- This will do the same as above, but use asn 123 as the origin
  - rtbh --advertise x.x.x.x --scope local -- This will advertise the prefix, but tag with the local communities
  - rtbh --list -- This will list the current routes being advertised
  - rtbh --withdraw x.x.x.x -- This will delete the announcement
