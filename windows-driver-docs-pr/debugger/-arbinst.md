---
title: arbinst
description: Arbinst 扩展显示有关指定仲裁器的信息。
keywords:
- 判
- arbinst Windows 调试
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- arbinst
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 25860eea8eed629441784fcf663536e3b159e5e1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800025"
---
# <a name="arbinst"></a>!arbinst


**！ Arbinst** 扩展显示有关指定仲裁器的信息。

```dbgcmd
    !arbinst Address [Flags]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="Address"></span><span id="address"></span><span id="ADDRESS"></span>*地址*  
指定要显示的仲裁器的十六进制地址。

<span id="Flags"></span><span id="flags"></span><span id="FLAGS"></span>*随意*  
指定要为每个仲裁器显示的信息量。 目前，唯一标志是0x100。 如果设置了此标志，则会显示别名。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>不可用</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息


另请参阅 [**！仲裁**](-arbiter.md) 器扩展。

<a name="remarks"></a>备注
-------

对于指定的仲裁程序， **！ arbinst** 显示系统资源的每个分配范围、一些可选标志、附加到该范围的 PDO (换言之，范围的所有者) ，以及此所有者 (（如果) 已知）的服务名称。

以下是示例：

```console
kd> !arbinst e0000106002ee8e8
Port Arbiter "PCI I/O Port (b=02)" at e0000106002ee8e8
  Allocated ranges:
    0000000000000000 - 0000000000001fff       00000000 <Not on bus>
    0000000000002000 - 00000000000020ff     P e0000000858bea20  (ql1280)
    0000000000003000 - ffffffffffffffff       00000000 <Not on bus>
  Possible allocation:
    < none >
kd> !arbinst e0000106002ec458
Memory Arbiter "PCI Memory (b=02)" at e0000106002ec458
  Allocated ranges:
    0000000000000000 - 00000000ebffffff       00000000 <Not on bus>
    00000000effdef00 - 00000000effdefff   B   e0000000858be560 
    00000000effdf000 - 00000000effdffff       e0000000858bea20  (ql1280)
    00000000f0000000 - ffffffffffffffff       00000000 <Not on bus>
  Possible allocation:
    < none >
```

 

 





