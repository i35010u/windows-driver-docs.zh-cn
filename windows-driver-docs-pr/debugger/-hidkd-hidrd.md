---
title: hidkd.hidrd
description: Hidkd.hidrd 命令显示在原始和已分析格式 HID 报表描述符。
ms.assetid: 8A9D76F2-7A36-4458-83A4-EDCB153EC45A
keywords:
- hidkd.hidrd Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- hidkd.hidrd
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1ef10fc0c2fb125fcec072f26ffc5f5501b8d217
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336486"
---
# <a name="hidkdhidrd"></a>!hidkd.hidrd


**！ Hidkd.hidrd**命令显示 HID 报表描述符中原始和已分析格式。

```dbgcmd
!hidkd.hidrd rd Length
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______rd______"></span><span id="_______RD______"></span> *rd*   
原始报表描述符数据的地址。 若要获取描述符数据地址，请使用[ **！ hidfdo** ](-hidkd-hidfdo.md)命令。

<span id="_______Length______"></span><span id="_______length______"></span><span id="_______LENGTH______"></span> *长度*   
将原始报表描述符数据长度 （字节）。 若要获取长度，请使用[ **！ hidfdo** ](-hidkd-hidfdo.md)命令。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Hidkd.dll

<a name="examples"></a>示例
--------

此示例演示如何使用[ **！ hidfdo** ](-hidkd-hidfdo.md)命令并后接 **！ hidrd**命令。 输出 **！ hidfdo**显示的地址和原始报表描述符数据的长度。

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

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[HID 的扩展](hid-extensions.md)

 

 






