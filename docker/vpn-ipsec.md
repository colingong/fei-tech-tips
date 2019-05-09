# vpn-ipsec

hwdsl2/ipsec-vpn-server比较好用，对手机，IOS设备，MACOS，直接可用。

对于WINDOWS客户端，要略微设置一下

```
docker run \
    --name ipsec-vpn-server \
    --env-file ./vpn.env \
    --restart=always \
    -p 500:500/udp \
    -p 4500:4500/udp \
    -v /lib/modules:/lib/modules:ro \
    -d --privileged \
    hwdsl2/ipsec-vpn-server

# 要注意udp的两个端口是不是开放，尤其安全组里有没有开放
```



vpn.env长这样：

```
# Define your own values for these variables
# - DO NOT put "" or '' around values, or add space around =
# - DO NOT use these special characters within values: \ " '

# VPN_IPSEC_PSK=your_ipsec_pre_shared_key
# VPN_USER=your_vpn_username
# VPN_PASSWORD=your_vpn_password

VPN_IPSEC_PSK=12345678901234567890
VPN_USER=fei

# 密码放这里，用明文
VPN_PASSWORD=xxx

# (Optional) Define additional VPN users
# - Uncomment and replace with your own values
# - Usernames and passwords must be separated by spaces
# VPN_ADDL_USERS=additional_username_1 additional_username_2
# VPN_ADDL_PASSWORDS=additional_password_1 additional_password_2
# (Optional) Use alternative DNS servers
# - By default, clients are set to use Google Public DNS
# - Example below shows using Cloudflare's DNS service
# VPN_DNS_SRV1=1.1.1.1
# VPN_DNS_SRV2=1.0.0.1
```



PPTPD本来也不错，对于一般情况用用没毛病，但是IOS/MAC升级后都不能直接支持，比较烦人，索性转到IPSEC搞定。