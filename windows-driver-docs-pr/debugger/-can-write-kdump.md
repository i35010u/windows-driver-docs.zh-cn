---
title: can_write_kdump
description: Can_write_kdump 扩展将验证目标计算机上是否有足够的磁盘空间来写入指定类型的内核转储文件。
keywords:
- 内核转储
- can_write_kdump Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- can_write_kdump
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4b87f694e7d159de6ab4f4621a11b7331ccbcb8e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814097"
---
# <a name="can_write_kdump"></a>！可以 \_ 编写 \_ kdump


**！可以 \_ 编写 \_ kdump** extension 验证目标计算机上是否有足够的磁盘空间来写入指定类型的内核转储文件。

```dbgsyntax
!can_write_kdump [-dn] [Options]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______-dn______"></span><span id="_______-DN______"></span>**-dn**   
指定目标计算机上的文件系统为 NTFS 文件系统。 如果省略此参数，则不能确定磁盘可用空间量，并且会显示一条警告。 但仍会显示所需的空间量。

<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span>*选项*   
以下选项是有效的：

<span id="-t"></span><span id="-T"></span>**-t**  
指定扩展应该确定是否有足够的空间用于小型转储。

<span id="-s"></span><span id="-S"></span>**-s**  
指定扩展应该确定是否有足够的空间用于汇总内核转储。 这是默认值。

<span id="-f"></span><span id="-F"></span>**-f**  
指定扩展应该确定是否有足够的空间用于完整的内核转储。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Kext.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Kext.dll</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

如果未指定任何 *选项* ，则扩展将确定是否有足够的空间用于汇总内核转储。

在以下示例中，未指定文件系统：

```dbgcmd
kd> !can_write_kdump
Checking kernel summary dump...
WARNING: Can't predict how many pages will be used, assuming worst-case.
Physical memory: 285560 KB
Page file size: 1572864 KB
NO: Page file too small
```

 

 





