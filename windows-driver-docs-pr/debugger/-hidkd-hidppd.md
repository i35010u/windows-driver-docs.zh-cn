---
title: hidkd.hidppd HID 扩展
description: Hidkd.hidppd 命令显示 HID preparsed 数据。
ms.assetid: 049D206D-669D-49F4-81FE-2D8E443F9A9E
keywords:
- hidkd.hidppd Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- hidkd.hidppd
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9a9cceb8130bc5e27a87eedec775aad6c3f0748f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548276"
---
# <a name="hidkdhidppd"></a>!hidkd.hidppd


**！ Hidkd.hidppd**命令显示 HID preparsed 数据。

```dbgcmd
!hidkd.hidppd ppd
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______ppd______"></span><span id="_______PPD______"></span> *ppd*   
地址**HIDP\_PREPARSED\_数据**结构。 若要获取的地址**HIDP\_PREPARSED\_数据**结构，请使用[ **！ hidfdo** ](-hidkd-hidfdo.md)或[ **！ hidpdo**](-hidkd-hidpdo.md).

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Hidkd.dll

<a name="examples"></a>示例
--------

此示例演示如何使用[ **！ hidpdo** ](-hidkd-hidpdo.md)跟 **！ hidppd**。 输出 **！ hidpdo**显示的地址**HIDP\_PREPARSED\_数据**结构。

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

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[HID 的扩展](hid-extensions.md)

 

 






