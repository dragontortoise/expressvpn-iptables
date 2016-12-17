*expressvpn-iptables*

Using iptables to prevent traffic to leak when ExpressVPN tunnel is broken. 

iptables script here is based on a blog post on jamielinux.com:

  Force all network traffic through OpenVPN using iptables

  https://jamielinux.com/blog/force-all-network-traffic-through-openvpn-
    using-iptables/

  (shorten url: https://goo.gl/T8T9YV )

ExpressVPN is a commercial OpenVPN service.  You can learn about it here:

  https://www.expressvpn.com

And if you want to sign up one, you can use my referal link below so that
both of us will earn a free 30 days from ExpressVPN:

  http://<span></span>www<span></span>.expressrefer.com/refer-a-friend/30-day
  s-free/?referrer\_id=9763644&utm\_campaign=referrals&utm\_medium=copy\_link
  &utm\_source=referral\_dashboard

  (shorten url: https://goo.gl/DSDUzn )

Like Jamie said:

  > Many people use OpenVPN to prevent snooping of their network traffic, such
  > as when connected to an untrusted wireless network. But how can you be sure
  > that no traffic ever leaks outside of the tunnel?
  > 
  > OpenVPN has a redirect-gateway option that directs all network traffic
  > through the tunnel; it replaces the existing default route (that usually
  > points to your local wireless router) with a new default route to the VPN
  > endpoint.
  >
  > It sounds perfect, but if the tunnel is broken unintentionally, the default
  > route may change back and cause traffic to leak.

The same is true for ExpressVPN as it uses OpenVPN.

This repository contains BASH shell script which can be used to prevent
such leak.

# Software environment

- Ubuntu Linux
- BASH
- OpenVPN
- ExpressVPN

# File structure

\*

|- readme.markdown : This file.

|- expressvpn-iptables : Script to be called right after ExpressVPN connection
    is established.  It will create iptables rules which will allow traffic to
    flow only when there is the active ExpressVPN connection.  If for any
    reason the ExpressVPN connection is disconnected, all traffic will be down
    hence preventing the data leak.

|- expressvpn-iptables-flush : Script to be called to clear all iptables rules
    created by expressvpn-iptables script.  Once iptables rules are cleared,
    all traffic don't have any restriction.

|- expressvpn-iptables.conf : Configuration file.

|- expressvpn-iptables.conf.template : Template file of the configuration
  file, expressvpn-iptables.conf.

|- expressvpn-iptables.local : Local iptables rules file.

|- expressvpn-iptables.local.template : Template file of the local iptables
  rules file, expressvpn-iptables.local.

# Install

1. Assuming you are inside expressvpn-iptables project directory.
2. `% mv expressvpn-iptables.conf.template expressvpn-iptables.conf` and
  edit the config file as needed.
3. `% mv expressvpn-iptables.local.template expressvpn-iptables.local` and
  edit the config file as needed.

# Recommended way of using ExpressVPN and expressvpn-iptables

1. Turn on your computer.  Make sure you don't open any programs which will
  connect to the Internet yet.  Assuming you are inside expressvpn-iptables
  project directory.
2. `% expressvpn connect`
3. `% sudo ./expressvpn-iptables`
4. Now you can use the Internet.
5. If for any reason the ExpressVPN connection is disconnected, you won't be
  able to use the Internet.  If you don't want to continue working, you can
  shutdown your computer now.  But if not, please continue to step 6.
6. Close all programs which use Internet connection.
7. `% sudo ./expressvpn-iptables-flush`
8. Go to step 2 and repeat the process.

