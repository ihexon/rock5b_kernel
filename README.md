# rock5b_kernel
Rock5B prebuild kernel with enhanced feature

## v1.2
Debian zramswap issue:
```
ihexon@rock-5b ~> sudo systemctl status zramswap.service
● zramswap.service - Linux zramswap setup
     Loaded: loaded (/lib/systemd/system/zramswap.service; enabled; vendor preset: enabled)
     Active: failed (Result: exit-code) since Mon 2022-10-24 14:33:42 UTC; 14s ago
       Docs: man:zramswap(8)
    Process: 2663107 ExecStart=/usr/sbin/zramswap start (code=exited, status=1/FAILURE)
   Main PID: 2663107 (code=exited, status=1/FAILURE)
        CPU: 182ms

Oct 24 14:33:42 rock-5b systemd[1]: Starting Linux zramswap setup...
Oct 24 14:33:42 rock-5b root[2663108]: Starting Zram
Oct 24 14:33:42 rock-5b zramswap[2663108]: <13>Oct 24 14:33:42 root: Starting Zram
Oct 24 14:33:42 rock-5b zramswap[2663110]: modprobe: FATAL: Module zram not found in directory /lib/modules/5.10.66-ge5e04a04b2bf
Oct 24 14:33:42 rock-5b root[2663111]: Error: inserting the zram kernel module
Oct 24 14:33:42 rock-5b zramswap[2663111]: <13>Oct 24 14:33:42 root: Error: inserting the zram kernel module
Oct 24 14:33:42 rock-5b systemd[1]: zramswap.service: Main process exited, code=exited, status=1/FAILURE
Oct 24 14:33:42 rock-5b systemd[1]: zramswap.service: Failed with result 'exit-code'.
Oct 24 14:33:42 rock-5b systemd[1]: Failed to start Linux zramswap setup.
```

Fixed by making zram as kernel modules, add `CONFIG_ZRAM_WRITEBACK=y` and `CONFIG_ZRAM_MEMORY_TRACKING=y`


- Support some USB Realtek rtlwifi

```
$ sha1sum *
1b750807031c322df163da1cfd16b288d13d7f32  88XXau.ko
ef86fd2a60adb4acd6e1f73ae96012e2b6230edb  8188gu.ko
da6377ae7a1c65c1c4fae4303668c575efeeae68  8821cu.ko
```
- Support some v4l2loopback
```
bd887c74cd68ca026ff4258e212ca93aff74c126  v4l2loopback.ko
```

## v1.1
- Support some USB Realtek rtlwifi
```
$ sha1sum *
8ba5579f60c3a94ee2e07ba6cbdd61f3c7462d05  88XXau.ko
47ecc0e56d35dab0569482d367507048ed602dfa  8188gu.ko
90557aa6ea01616ca0731ce7a90ed41876fba0b8  8821cu.ko
```

- Open Security options to support eBPF trace code
```
CONFIG_KEYS=y
CONFIG_TRUSTED_KEYS=m
CONFIG_ENCRYPTED_KEYS=m
CONFIG_KEY_DH_OPERATIONS=y
CONFIG_SECURITY_DMESG_RESTRICT=y
CONFIG_SECURITY=y
CONFIG_SECURITYFS=y
CONFIG_SECURITY_NETWORK=y
CONFIG_SECURITY_NETWORK_XFRM=y
CONFIG_SECURITY_PATH=y
CONFIG_HAVE_HARDENED_USERCOPY_ALLOCATOR=y
```

## v1.0
- Add nf_table framework and bridge_netfilter which needed by docker
```
CONFIG_NF_CONNTRACK_BRIDGE=m
CONFIG_BRIDGE_NF_EBTABLES=m
CONFIG_NF_NAT_SNMP_BASIC=m
CONFIG_NF_NAT_PPTP=m
CONFIG_NF_NAT_H323=m
CONFIG_IP_NF_IPTABLES=m
CONFIG_IP_NF_MATCH_AH=m
CONFIG_IP_NF_MATCH_ECN=m
CONFIG_IP_NF_MATCH_RPFILTER=m
CONFIG_IP_NF_MATCH_TTL=m
CONFIG_IP_NF_FILTER=m
CONFIG_IP_NF_TARGET_REJECT=m
CONFIG_IP_NF_TARGET_SYNPROXY=m
CONFIG_IP_NF_NAT=m
CONFIG_IP_NF_TARGET_MASQUERADE=m
CONFIG_IP_NF_TARGET_NETMAP=m
CONFIG_IP_NF_TARGET_REDIRECT=m
CONFIG_IP_NF_MANGLE=m
CONFIG_IP_NF_TARGET_CLUSTERIP=m
CONFIG_IP_NF_TARGET_ECN=m
CONFIG_IP_NF_TARGET_TTL=m
CONFIG_IP_NF_RAW=m
```
