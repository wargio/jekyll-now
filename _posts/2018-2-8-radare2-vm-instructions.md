---
layout: post
title: radare2 and vpcext
---

radare2 is now capable to decompile the following "instructions"

```
0F C6 28 01 00     vmcpuid
0F C6 28 00 00     vmgetinfo
0F C6 28 00 01     vmsetinfo
0F C6 28 00 02     vmdxdsbl
0F C6 28 00 03     vmdxenbl
0F C6 28 01 00     vmcpuid
0F C6 28 01 01     vmhlt
0F C6 28 01 02     vmsplaf
0F C6 28 02 00     vmpushfd
0F C6 28 02 01     vmpopfd
0F C6 28 02 02     vmcli
0F C6 28 02 03     vmsti
0F C6 28 02 04     vmiretd
0F C6 28 03 00     vmsgdt
0F C6 28 03 01     vmsidt
0F C6 28 03 02     vmsldt
0F C6 28 03 03     vmstr
0F C6 28 04 00     vmsdte
0F 3F 01 XX        vpcext 01h XXh
0F 3F 05 XX        vpcext 05h XXh
0F 3F 07 XX        vpcext 07h XXh
0F 3F 0D XX        vpcext 0Dh XXh
0F 3F 10 XX        vpcext 10h XXh
```

You can see the commit [here](https://github.com/radare/radare2/pull/9350)

![_config.yml]({{ site.baseurl }}/images/vpcext.jpg)

`Derived from a function in a notpetya sample binary`

[Twitter Share](https://twitter.com/Der0ad/status/961750815915393024)