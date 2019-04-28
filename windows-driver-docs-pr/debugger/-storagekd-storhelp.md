---
title: storagekd.storhelp
description: Storagekd.storhelp 扩展显示 Storagekd.dll 扩展命令的帮助文本。
ms.assetid: 17FFB5CC-1FA3-4D13-AA30-6D48D2435CDC
keywords:
- storagekd.storhelp Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- storagekd.storhelp
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2a80107f063e87031221d5364418831cd668e940
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338800"
---
# <a name="storagekdstorhelp"></a>!storagekd.storhelp


**！ Storagekd.storhelp**扩展显示 Storagekd.dll 扩展命令的帮助文本。

```dbgcmd
!storagekd.storhelp 
```

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 8 及更高版本</strong></p></td>
<td align="left"><p>Storagekd.dll</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

下面是举例 **！ storagekd.storhelp**显示：

**0: kd&gt; !storagekd.storhelp**

```dbgcmd
# Storage Debugger Extension
===============================================
## General Commands
----------------
!storhelp    - Displays complete help of the commands provided in this KD extension
!storclass   - Dumps all class devices managed by classpnp
!storadapter - Dumps all adapters managed by Storport
!storunit    - Dumps all disks managed by Storport

## STORPORT specific commands
--------------------------
!storlogirp <args>     - displays internal log entries that reference the specified IRP.
                         See '!storhelp storlogirp' for details.
!storloglist <args>    - displays internal log entries. See '!storhelp storloglist' for details.
!storlogsrb <args>     - displays internal log entries that reference the specified SRB.
                         See '!storhelp storlogsrb' for details.
!storsrb <address>     - display details for the specified SCSI or STORAGE request block
```

 

 





