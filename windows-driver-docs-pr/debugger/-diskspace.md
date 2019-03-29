---
title: 磁盘空间
description: 磁盘空间扩展显示目标计算机的硬盘上的可用空间量。
ms.assetid: 9153cdc0-addf-4804-a898-1e4280ac60ea
keywords:
- Windows 调试的磁盘空间
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- diskspace
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e79917aa3e0109e4c78b7c33c827c08ce2c8f64a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567698"
---
# <a name="diskspace"></a>!diskspace


**！ 磁盘空间**扩展插件都会显示在目标计算机的硬盘上的可用空间量。

```dbgcmd
!diskspace Drive[:]
```

## <a name="span-idddkdiskspacedbgspanspan-idddkdiskspacedbgspanparameters"></a><span id="ddk__diskspace_dbg"></span><span id="DDK__DISKSPACE_DBG"></span>参数


<span id="_______Drive______"></span><span id="_______drive______"></span><span id="_______DRIVE______"></span> *Drive*   
指定磁盘的驱动器号。 冒号 （:）后*驱动器*是可选的。

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

下面是一个示例：

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

 

 





