                  |  OpenVPN  |   ShadowSocks  | ShadowVPN
----------------- | --------- | -------------- | ----------
Layer             |     IP    |     TCP/UDP    |     IP
Frontend          |    VPN    | socks/iptables |    VPN
Security          |    CCA    |       CPA      |    CCA
Protocol Sniffing |  possible |    difficult   | difficult
Tamper Proof      |     Y     |        N       |     Y
Disruption Proof  |     N     |        N       |     Y
Speed             | fast(UDP) |       fast     |    fast
CPU utilization   |    high   |      medium    |    low
RAM               |    low    |      medium    |    low

ShadowVPN is inspired by SigmaVPN:
- Stateless VPN
- Low resource comsumption

ShadowVPN has several improvements over SigmaVPN:
- Faster encryption
- Use multiple UDP sockets
- User friendly configuration with scripting support
- Builtin daemon and logging support
- Lower packet overhead
- Does not crash easily
- Use GNU Autotools, making it easier to build and port