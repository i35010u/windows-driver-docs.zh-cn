---
title: hidkd.hidrd
description: Hidkd. hidrd 命令以原始格式和已分析格式显示 HID 报表说明符。
keywords:
- hidkd hidrd Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- hidkd.hidrd
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: bbc2218e4d307ee96329d983b4022b0556797ca5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821049"
---
# <a name="hidkdhidrd"></a>!hidkd.hidrd


**！ Hidkd. hidrd** 命令以原始格式和已分析格式显示 HID 报表说明符。

```dbgcmd
!hidkd.hidrd rd Length
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______rd______"></span><span id="_______RD______"></span>*rd*   
原始报表描述符数据的地址。 若要获取描述符数据的地址，请使用 [**！ hidfdo**](-hidkd-hidfdo.md) 命令。

<span id="_______Length______"></span><span id="_______length______"></span><span id="_______LENGTH______"></span>*长度*   
原始报表描述符数据的长度（以字节为单位）。 若要获取长度，请使用 [**！ hidfdo**](-hidkd-hidfdo.md) 命令。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


Hidkd.dll

<a name="examples"></a>示例
--------

此示例演示如何使用后跟 **！ hidrd** 命令的 [**！ hidfdo**](-hidkd-hidfdo.md)命令。 **！ Hidfdo** 的输出显示原始报表描述符数据的地址和长度。

```dbgcmd
0: kd> !hidfdo 0xffffe00004f466e0
# FDO 0xffffe00004f466e0  (!devobj/!devstack)

  Name              : \Device\_HID00000002
  ...
  Report Descriptor : !hidrd 0xffffe00004281a80 0x127
  ...

0: kd> !hidrd 0xffffe00004281a80 0x127
Report Descriptor at 0xffffe00004281a80

## Raw Data

0x0000: 05 01 09 02 A1 01 05 01-09 02 A1 02 85 1A 09 01
0x0010: A1 00 05 09 19 01 29 05-95 05 75 01 15 00 25 01
0x0020: 81 02 75 03 95 01 81 01-05 01 09 30 09 31 95 02
...

## Parsed

Usage Page (Generic Desktop Controls)....................0x0000: 05 01
Usage (Mouse)............................................0x0002: 09 02
Collection (Application).................................0x0004: A1 01
..Usage Page (Generic Desktop Controls)..................0x0006: 05 01
..Usage (Mouse)..........................................0x0008: 09 02
..Collection (Logical)...................................0x000A: A1 02
....Report ID (26).......................................0x000C: 85 1A
...
End Collection ()........................................0x0126: C0
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[HID 扩展](hid-extensions.md)

 

 






