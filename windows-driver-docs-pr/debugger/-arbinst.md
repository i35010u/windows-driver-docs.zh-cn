---
title: arbinst
description: Arbinst 扩展显示有关指定仲裁器的信息。
ms.assetid: 6aa06283-9cd7-4579-9e5d-40bbaf53f782
keywords:
- 仲裁器
- arbinst Windows 调试
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- arbinst
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2e4f4d1161fbfa5b167c0b82fb96274d44b158f0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546690"
---
# <a name="arbinst"></a>！ arbinst


**！ Arbinst**扩展显示有关指定仲裁器的信息。

```dbgcmd
    !arbinst Address [Flags]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="Address"></span><span id="address"></span><span id="ADDRESS"></span>*Address*  
指定仲裁器要显示的十六进制地址。

<span id="Flags"></span><span id="flags"></span><span id="FLAGS"></span>*标志*  
指定要为每个仲裁器显示多少信息。 目前，唯一标志是 0x100。 如果设置此标志，则会显示别名。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


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

 

## <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息


另请参阅[ **！ arbiter** ](-arbiter.md)扩展。

<a name="remarks"></a>备注
-------

仲裁器指定，对于 **！ arbinst**显示每个分配范围的系统资源，某些可选标志，PDO 附加到该范围 （即，该范围的所有者），并且此所有者的服务名称 （如果已知）。

下面是一个示例：

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

 

 





