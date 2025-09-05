---
title: Mihomo配置模板
pubDate: 2025-09-05
categories: ['折腾']
description: ''
---

```
mode: rule
ipv6: true
log-level: info
allow-lan: true
mixed-port: 8888
unified-delay: true
tcp-concurrent: true
external-controller: :9090
external-ui: ui
external-ui-url: "https://github.com/Zephyruso/zashboard/archive/refs/heads/gh-pages.zip"
geodata-mode: true
geox-url:
  geoip: "https://fastly.jsdelivr.net/gh/MetaCubeX/meta-rules-dat@release/geoip.dat"
  geosite: "https://fastly.jsdelivr.net/gh/MetaCubeX/meta-rules-dat@release/geosite.dat"
  mmdb: "https://fastly.jsdelivr.net/gh/MetaCubeX/meta-rules-dat@release/geoip.metadb"
find-process-mode: strict
keep-alive-interval: 1800
global-client-fingerprint: random
profile:
  store-selected: true
  store-fake-ip: true
sniffer:
  enable: true
  sniff:
    TLS:
      ports: [443, 8443]
    HTTP:
      ports: [80, 8080-8880]
      override-destination: true
tun:
  enable: false  #true
  stack: system  #gvisor
  dns-hijack:
    - "any:53"
    - "tcp://any:53"
  auto-route: true
  auto-detect-interface: true

dns:
  enable: true
  listen: :1053
  ipv6: true
  enhanced-mode: fake-ip
  fake-ip-range: 28.0.0.1/8
  fake-ip-filter:
    - '*'
    - '+.lan'
    - '+.local'
  nameserver:
    - 119.29.29.29
    - 223.5.5.5
    - 114.114.114.114
    - '[2402:4e00::]'
    - '[2400:3200::1]'

proxy-providers:
  Cloud:
    type: http
    path: ./proxy_provider/Cloud.yaml
    url: "填入订阅链接"
    interval: 86400
    health-check:
      enable: true
      url: "http://cp.cloudflare.com/generate_204"
      interval: 30

proxy-groups:
  - name: Proxy
    type: select
    proxies: 
      - Hong Kong
      - Japan
      - United States
      - Singapore
      - AllServer
  - name: YouTube
    type: select
    proxies:
      - Hong Kong
      - Japan
      - United States
      - Singapore
      - AllServer
  - name: Telegram
    type: select
    proxies:
      - Hong Kong
      - Japan
      - United States
      - Singapore
      - AllServer
  - name: Steam
    type: select
    proxies:
      - Proxy
      - AllServer
  - name: Speedtest
    type: select
    proxies:
      - Proxy
      - DIRECT
  - name: AI
    type: select
    proxies:
      - Hong Kong
      - Japan
      - United States
      - Singapore
      - AllServer
  #######################
  - name: Hong Kong
    type: url-test
    url: "http://cp.cloudflare.com/generate_204"
    interval: 1800
    tolerance: 2
    filter: '🇭🇰|港'
    use:
      - Cloud
  - name: Japan
    type: url-test
    url: "http://cp.cloudflare.com/generate_204"
    interval: 1800
    tolerance: 2
    filter: '🇯🇵|日'
    use:
      - Cloud
  - name: United States
    type: url-test
    url: "http://cp.cloudflare.com/generate_204"
    interval: 1800
    tolerance: 2
    filter: '🇺🇸|美'
    use:
      - Cloud
  - name: Singapore
    type: url-test
    url: "http://cp.cloudflare.com/generate_204"
    interval: 1800
    tolerance: 2
    filter: '🇸🇬|坡'
    use:
      - Cloud
  - name: AllServer
    type: select
    filter: '^((?!(流量|重置|套餐|网址)).)*$'
    use:
      - Cloud

rule-providers:
  AWAvenue-Ads:
    type: http
    behavior: classical
    url: "https://raw.githubusercontent.com/TG-Twilight/AWAvenue-Ads-Rule/refs/heads/main/Filters/AWAvenue-Ads-Rule-Clash-Classical.yaml"
    path: ./Rules/AWAvenue-Ads
    interval: 86400
    proxy: Proxy
  YouTube:
    type: http
    behavior: classical
    url: 'https://raw.githubusercontent.com/blackmatrix7/ios_rule_script/master/rule/Clash/YouTube/YouTube.yaml'
    path: ./Rules/YouTube
    interval: 86400
    proxy: Proxy
  Telegram:
    type: http
    behavior: classical
    url: 'https://raw.githubusercontent.com/blackmatrix7/ios_rule_script/master/rule/Clash/Telegram/Telegram.yaml'
    path: ./Rules/Telegram
    interval: 86400
    proxy: Proxy
  SteamCN:
    type: http
    behavior: classical
    url: 'https://raw.githubusercontent.com/blackmatrix7/ios_rule_script/master/rule/Clash/SteamCN/SteamCN.yaml'
    path: ./Rules/SteamCN
    interval: 86400
    proxy: Proxy
  Steam:
    type: http
    behavior: classical
    url: 'https://raw.githubusercontent.com/blackmatrix7/ios_rule_script/master/rule/Clash/Steam/Steam.yaml'
    path: ./Rules/Steam
    interval: 86400
    proxy: Proxy
  Speedtest:
    type: http
    behavior: classical
    url: 'https://raw.githubusercontent.com/blackmatrix7/ios_rule_script/master/rule/Clash/Speedtest/Speedtest.yaml'
    path: ./Rules/Speedtest
    interval: 86400
    proxy: Proxy
  Bing:
    type: http
    behavior: classical
    url: 'https://raw.githubusercontent.com/blackmatrix7/ios_rule_script/master/rule/Clash/Bing/Bing.yaml'
    path: ./Rules/Bing
    interval: 86400
    proxy: Proxy
  Gemini:
    type: http
    behavior: classical
    url: 'https://raw.githubusercontent.com/blackmatrix7/ios_rule_script/master/rule/Clash/Gemini/Gemini.yaml'
    path: ./Rules/Gemini
    interval: 86400
    proxy: Proxy
  OpenAI:
    type: http
    behavior: classical
    url: 'https://raw.githubusercontent.com/blackmatrix7/ios_rule_script/master/rule/Clash/OpenAI/OpenAI.yaml'
    path: ./Rules/OpenAI
    interval: 86400
    proxy: Proxy
  GitHub:
    type: http
    behavior: classical
    url: 'https://raw.githubusercontent.com/blackmatrix7/ios_rule_script/master/rule/Clash/GitHub/GitHub.yaml'
    path: ./Rules/GitHub
    interval: 86400
    proxy: Proxy
  PROXY:
    type: http
    behavior: classical
    url: 'https://raw.githubusercontent.com/blackmatrix7/ios_rule_script/master/rule/Clash/Proxy/Proxy_Classical.yaml'
    path: ./Rules/Proxy
    interval: 86400
    proxy: Proxy
  LAN:
    type: http
    behavior: classical
    url: 'https://raw.githubusercontent.com/blackmatrix7/ios_rule_script/master/rule/Clash/Lan/Lan.yaml'
    path: ./Rules/LAN
    interval: 86400
    proxy: Proxy

rules:
  - RULE-SET,AWAvenue-Ads,REJECT
  - DOMAIN-SUFFIX,dogfight360.com,DIRECT
  - RULE-SET,YouTube,YouTube
  - RULE-SET,Telegram,Telegram
  - RULE-SET,SteamCN,DIRECT
  - RULE-SET,Steam,Steam
  - RULE-SET,Speedtest,Speedtest
  - RULE-SET,Bing,AI
  - RULE-SET,Gemini,AI
  - RULE-SET,OpenAI,AI
  - RULE-SET,GitHub,Proxy
  - RULE-SET,PROXY,Proxy
  - RULE-SET,LAN,DIRECT
  - GEOIP,CN,DIRECT
  - MATCH,Proxy
```