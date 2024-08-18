socks-port: 7891
redir-port: 7892
mixed-port: 7893
mode: rule
log-level: silent
allow-lan: true
external-controller: 0.0.0.0:9090
bind-address: "*"
ipv6: false
dns:
  enable: true
  ipv6: false
  enhanced-mode: redir-host
  listen: 0.0.0.0:7894
  fallback-filter:
    geoip: false
    ipcidr:
    - 240.0.0.0/4
  nameserver:
    - https://puredns.org/dns-query
    - tls://puredns.org:853
  fallback:
    - tcp://108.137.44.39
    - tcp://108.137.44.9
    - 108.137.44.39
    - 108.137.44.9
tun:
  enable: true
  stack: system 
  macOS-auto-route: true
  macOS-auto-detect-interface: true
  dns-hijack:
    - tcp://108.137.44.39:53
experimental:
  interface-name: en0

proxies:
 - {name: TROJANKMSP1, server: 104.17.3.81, port: 443, udp: true, type: trojan, password: e062cd20-22eb-4fab-ab7c-03921b065439, sni: sg-trojan-vvip-14.topvpn.my.id, skip-cert-verify: true, network: ws, ws-opts: {path: /websocket-trojan, headers: {Host: sg-trojan-vvip-14.topvpn.my.id}}}

proxy-groups:
 - name: kmspstore-generator
   type: select
   proxies:
    - TROJANKMSP1
rules:
 - MATCH,kmspstore-generator
