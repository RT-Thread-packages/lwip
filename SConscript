from building import *

src = Split("""
src/api/api_lib.c
src/api/api_msg.c
src/api/err.c
src/api/netbuf.c
src/api/netdb.c
src/api/netifapi.c
src/api/sockets.c
src/api/tcpip.c
src/core/def.c
src/core/dns.c
src/core/inet_chksum.c
src/core/init.c
src/core/ip.c
src/core/memp.c
src/core/netif.c
src/core/pbuf.c
src/core/raw.c
src/core/stats.c
src/core/sys.c
src/core/tcp.c
src/core/tcp_in.c
src/core/tcp_out.c
src/core/timeouts.c
src/core/udp.c
src/netif/ethernet.c
src/netif/lowpan6.c
""")

ipv4_src = Split("""
src/core/ipv4/autoip.c
src/core/ipv4/dhcp.c
src/core/ipv4/etharp.c
src/core/ipv4/icmp.c
src/core/ipv4/igmp.c
src/core/ipv4/ip4.c
src/core/ipv4/ip4_addr.c
src/core/ipv4/ip4_frag.c
""")

ipv6_src = Split("""
src/core/ipv6/dhcp6.c
src/core/ipv6/ethip6.c
src/core/ipv6/icmp6.c
src/core/ipv6/inet6.c
src/core/ipv6/ip6.c
src/core/ipv6/ip6_addr.c
src/core/ipv6/ip6_frag.c
src/core/ipv6/mld6.c
src/core/ipv6/nd6.c
""")

snmp_src = Glob("src/apps/snmp/*.c")

ppp_src = Glob("src/netif/ppp/*.c") + Glob("src/netif/ppp/polarssl/*c")

src = src + ipv4_src

# The set of source files associated with this SConscript file.
path = [GetCurrentDir() + '/src/include',
    GetCurrentDir() + '/src/include/ipv4',
    GetCurrentDir() + '/src/include/netif']

if not GetDepend('RT_USING_SAL'):
    path += [GetCurrentDir() + '/src/include/posix']

if GetDepend(['RT_LWIP_SNMP']):
    src += snmp_src
    path += [GetCurrentDir() + '/src/apps/snmp']

if GetDepend(['RT_LWIP_PPP']):
    src += ppp_src
    path += [GetCurrentDir() + '/src/netif/ppp']

if GetDepend(['RT_USING_LWIP_IPV6']):
    src += ipv6_src

if GetDepend(['RT_LWIP_USING_PING']):
    src += Glob('src/apps/ping/ping.c')

group = DefineGroup('lwIP', src, depend = ['RT_USING_LWIP', 'RT_USING_LWIP203'], CPPPATH = path)

Return('group')
