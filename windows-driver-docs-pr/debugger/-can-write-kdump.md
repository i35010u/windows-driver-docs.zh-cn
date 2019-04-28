---
title: can_write_kdump
description: Can_write_kdump 扩展验证要写入指定类型的内核转储文件的目标计算机上没有足够的磁盘空间。
ms.assetid: e9fdf8a4-3294-4625-a854-5e42a69374a6
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
ms.openlocfilehash: 0449a7a28fcf85deb17e08f1932bb55d7ea23f5c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336904"
---
# <a name="canwritekdump"></a>!can\_write\_kdump


**！ 可以\_编写\_kdump**扩展验证要写入指定类型的内核转储文件的目标计算机上是否存在足够的磁盘空间。

```dbgsyntax
!can_write_kdump [-dn] [Options]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______-dn______"></span><span id="_______-DN______"></span> **-dn**   
指定目标计算机上的文件系统为 NTFS 文件系统。 如果省略此参数，则不能确定磁盘可用空间量，并将显示一条警告。 但是，仍将显示所需的空间量。

<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *选项*   
以下选项是有效的：

<span id="-t"></span><span id="-T"></span>**-t**  
指定该扩展应确定是否有足够的空间用于小型转储。

<span id="-s"></span><span id="-S"></span>**-s**  
指定该扩展应确定是否有足够的空间用于摘要内核转储。 这是默认值。

<span id="-f"></span><span id="-F"></span>**-f**  
指定该扩展应确定是否有足够的空间用于完整核心转储。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

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

如果没有*选项*指定，则该扩展将确定是否有足够的空间用于摘要内核转储。

在以下示例中，未指定文件系统：

```dbgcmd
kd> !can_write_kdump
Checking kernel summary dump...
WARNING: Can't predict how many pages will be used, assuming worst-case.
Physical memory: 285560 KB
Page file size: 1572864 KB
NO: Page file too small
```

 

 





