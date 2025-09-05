---
title: Surge配置模板
pubDate: 2025-09-05
categories: ['折腾']
description: ''
---

```
[General]
http-listen = 0.0.0.0:8888
socks5-listen = 0.0.0.0:8889
loglevel = notify
allow-wifi-access = true
show-error-page-for-reject = true
ipv6 = true
ipv6-vif = auto
test-timeout = 3
internet-test-url = http://cp.cloudflare.com/generate_204
proxy-test-url = http://cp.cloudflare.com/generate_204
dns-server = 2402:4e00::, 2400:3200::1, 119.29.29.29, 223.5.5.5
# encrypted-dns-server = https://doh.pub/dns-query, https://dns.alidns.com/dns-query
hijack-dns = 8.8.8.8:53, 8.8.4.4:53
skip-proxy = 127.0.0.1, 192.168.0.0/16, 10.0.0.0/8, 172.16.0.0/12, 100.64.0.0/10, 17.0.0.0/8, localhost, *.local
always-real-ip = *.srv.nintendo.net, *.stun.playstation.net, xbox.*.microsoft.com, *.xboxlive.com, *.battlenet.com.cn, *.battlenet.com, *.blzstatic.cn, *.battle.net
exclude-simple-hostnames = true
use-default-policy-if-wifi-not-primary = false
udp-policy-not-supported-behaviour = reject

[Proxy Group]
Proxy = select, Hong Kong, Japan, United States, Singapore, AllServer
YouTube = select, Hong Kong, Japan, United States, Singapore, AllServer
Telegram = select, Hong Kong, Japan, United States, Singapore, AllServer
Steam = select, Proxy, AllServer
Speedtest = select, Proxy, DIRECT
AI = select, Hong Kong, Japan, United States, Singapore, AllServer
Hong Kong = smart, include-other-group="Cloud", policy-regex-filter=🇭🇰|港
Japan = smart, include-other-group="Cloud", policy-regex-filter=🇯🇵|日
United States = smart, include-other-group="Cloud", policy-regex-filter=🇺🇸|美
Singapore = smart, include-other-group="Cloud", policy-regex-filter=🇸🇬|坡
AllServer = select, include-other-group="Cloud"
Cloud = select, policy-path=粘贴订阅, hidden=1, update-interval=86400, policy-regex-filter=^((?!(流量|重置|套餐|网址)).)*$
[Rule]
DOMAIN-SUFFIX,dogfight360.com,DIRECT
RULE-SET,https://raw.githubusercontent.com/blackmatrix7/ios_rule_script/master/rule/Surge/YouTube/YouTube.list,YouTube
RULE-SET,https://raw.githubusercontent.com/blackmatrix7/ios_rule_script/master/rule/Surge/Telegram/Telegram.list,Telegram
RULE-SET,https://raw.githubusercontent.com/blackmatrix7/ios_rule_script/master/rule/Surge/SteamCN/SteamCN.list,DIRECT
RULE-SET,https://raw.githubusercontent.com/blackmatrix7/ios_rule_script/master/rule/Surge/Steam/Steam.list,Steam
RULE-SET,https://raw.githubusercontent.com/blackmatrix7/ios_rule_script/master/rule/Surge/Speedtest/Speedtest.list,Speedtest
RULE-SET,https://raw.githubusercontent.com/blackmatrix7/ios_rule_script/master/rule/Surge/Apple/Apple_All.list,Proxy
RULE-SET,https://raw.githubusercontent.com/blackmatrix7/ios_rule_script/master/rule/Surge/Bing/Bing.list,AI
RULE-SET,https://raw.githubusercontent.com/blackmatrix7/ios_rule_script/master/rule/Surge/Gemini/Gemini.list,AI
RULE-SET,https://raw.githubusercontent.com/blackmatrix7/ios_rule_script/master/rule/Surge/OpenAI/OpenAI.list,AI
RULE-SET,https://raw.githubusercontent.com/blackmatrix7/ios_rule_script/master/rule/Surge/GitHub/GitHub.list,Proxy
RULE-SET,https://raw.githubusercontent.com/blackmatrix7/ios_rule_script/master/rule/Surge/Proxy/Proxy_All.list,Proxy,extended-matching
RULE-SET,https://raw.githubusercontent.com/blackmatrix7/ios_rule_script/master/rule/Surge/Lan/Lan.list,DIRECT
GEOIP,CN,DIRECT
FINAL,Proxy,dns-failed
```