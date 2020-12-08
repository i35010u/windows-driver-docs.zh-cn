---
title: hidkd. hidppd HID 扩展
description: Hidkd. hidppd 命令显示 HID preparsed 数据。
keywords:
- hidkd hidppd Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- hidkd.hidppd
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7f4793b84712b24ffb002e5a68cc851d7ca891d1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825835"
---
# <a name="hidkdhidppd"></a>!hidkd.hidppd


**！ Hidkd. hidppd** 命令显示 HID preparsed 数据。

```dbgcmd
!hidkd.hidppd ppd
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______ppd______"></span><span id="_______PPD______"></span>*ppd*   
**HIDP \_ PREPARSED \_ 数据** 结构的地址。 若要获取 **HIDP \_ PREPARSED \_ 数据** 结构的地址，请使用 [**！ hidfdo**](-hidkd-hidfdo.md) 或 [**！ hidpdo**](-hidkd-hidpdo.md)。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


Hidkd.dll

<a name="examples"></a>示例
--------

此示例演示如何使用 [**！ hidpdo**](-hidkd-hidpdo.md) 后跟 **！ hidppd**。 **！ Hidpdo** 的输出显示 **HIDP \_ PREPARSED \_ 数据** 结构的地址。

```dbgcmd

0: kd> !hidpdo 0xffffe000029f6060
## PDO 0xffffe000029f6060  (!devobj/!devstack)

  Collection Num  : 1
  Name            : \Device\_HID00000000#COLLECTION00000001
  ...
  Pre-parsed Data : 0xffffe000029d1010
  ...

0: kd> !hidkd.hidppd 0xffffe000029d1010
Reading preparsed data...
Preparsed Data at 0xffffe000029d1010  

## Summary

  UsagePage             : Vendor-defined (0xFFA0)
  Usage                 : 0x01
  Report Length         : 0x2(Input) 0x2(Output) 0x0(Feature)
  Link Collection Nodes : 2
  Button Caps           : 0(Input) 0(Output) 0(Feature)
  Value Caps            : 1(Input) 1(Output) 0(Feature)
  Data Indices          : 1(Input) 1(Output) 0(Feature)

## Input Value Capability #0

  Report ID         : 0x0
  Usage Page        : Vendor-defined (0xFFA1)
  Bit Size          : 0x8
  Report Count      : 0x1
  ...
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[HID 扩展](hid-extensions.md)

 

 






