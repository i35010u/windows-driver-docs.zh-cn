---
title: 磁盘
description: 磁盘空间扩展显示目标计算机的硬盘上的可用空间量。
keywords:
- 磁盘空间 Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- diskspace
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5661da75cfd00762f65d002766a1c7d8c5add82a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805895"
---
# <a name="diskspace"></a>!diskspace


**！磁盘** 空间扩展显示目标计算机的硬盘上的可用空间量。

```dbgcmd
!diskspace Drive[:]
```

## <a name="span-idddk__diskspace_dbgspanspan-idddk__diskspace_dbgspanparameters"></a><span id="ddk__diskspace_dbg"></span><span id="DDK__DISKSPACE_DBG"></span>参数


<span id="_______Drive______"></span><span id="_______drive______"></span><span id="_______DRIVE______"></span>*驱动器*   
指定磁盘的驱动器号。 冒号 (： *驱动器* 后 ) 是可选的。

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

以下是示例：

```dbgcmd
kd> !diskspace c:
Checking Free Space for c: ..........
   Cluster Size 0 KB
 Total Clusters 4192901 KB
  Free Clusters 1350795 KB
    Total Space 1 GB (2096450 KB)
     Free Space 659.567871 MB (675397 KB)

kd> !diskspace f:
Checking Free Space for f: 
f: is a CDROM drive. This function is not supported!
```

 

 





