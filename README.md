# Description
The `smb` service contains a memory corruption vulnerability. Remote, unauthenticated attackers can exploit this issue by sending specially crafted packets, triggering a null pointer dereference. This leads to a Remote Denial of Service (DoS), rendering the `smb` service unavailable.

```
2024.11.20-23:14:36.78@0: /nova/bin/smb
2024.11.20-23:14:36.78@0: --- signal=11 --------------------------------------------
2024.11.20-23:14:36.78@0: 
2024.11.20-23:14:36.78@0: eip=0x080616c0 eflags=0x00010212
2024.11.20-23:14:36.78@0: edi=0x00000000 esi=0x88c85074 ebp=0x7fe66ce8 esp=0x7fe66cb0
2024.11.20-23:14:36.78@0: eax=0x7f4000ec ebx=0x08085168 ecx=0x08085070 edx=0x80c00004
2024.11.20-23:14:36.78@0: 
2024.11.20-23:14:36.78@0: maps:
2024.11.20-23:14:36.78@0: 08048000-08071000 r-xp 00000000 00:0c 1454                               /nova/bin/smb
2024.11.20-23:14:36.78@0: 77713000-77748000 r-xp 00000000 00:0c 1276                               /lib/libuClibc-0.9.33.2.so
2024.11.20-23:14:36.78@0: 7774c000-77766000 r-xp 00000000 00:0c 1272                               /lib/libgcc_s.so.1
2024.11.20-23:14:36.78@0: 77767000-77776000 r-xp 00000000 00:0c 1256                               /lib/libuc++.so
2024.11.20-23:14:36.78@0: 77777000-7777b000 r-xp 00000000 00:0c 1260                               /lib/libucrypto.so
2024.11.20-23:14:36.78@0: 7777c000-777c7000 r-xp 00000000 00:0c 1258                               /lib/libumsg.so
2024.11.20-23:14:36.78@0: 777ca000-777d2000 r-xp 00000000 00:0c 1262                               /lib/libubox.so
2024.11.20-23:14:36.78@0: 777d6000-777dd000 r-xp 00000000 00:0c 1270                               /lib/ld-uClibc-0.9.33.2.so
2024.11.20-23:14:36.78@0: 
2024.11.20-23:14:36.78@0: stack: 0x7fe67000 - 0x7fe66cb0 
2024.11.20-23:14:36.78@0: 00 00 00 00 00 00 00 00 00 00 00 00 68 51 08 08 c4 46 07 08 00 00 00 00 08 6d e6 7f bc 60 05 08 
2024.11.20-23:14:36.78@0: 04 00 00 00 50 00 00 00 08 6d e6 7f 68 51 08 08 b8 46 07 08 00 00 00 00 18 6d e6 7f 84 e3 05 08 
2024.11.20-23:14:36.78@0: 
2024.11.20-23:14:36.78@0: code: 0x80616c0
2024.11.20-23:14:36.78@0: 8b 3e 66 c1 c7 08 c1 c7 10 66 c1 c7 08 81 ff 42 
2024.11.20-23:14:36.78@0: 
2024.11.20-23:14:36.78@0: backtrace: 0x080616c0 0x0805e384 0x0805e3d4 0x0805e3ad 0x0805e6b2 0x7779dc4b 0x7779dca3 0x777a4745 0x0804d827 
2024.11.20-23:14:36.78@0: 
```

# Affected Version
This vulnerability was initially found in RouterOS stable `6.40.5`.
