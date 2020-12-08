---
title: storagekd.storhelp
description: Storagekd. storhelp 扩展显示 Storagekd.dll 扩展命令的帮助文本。
keywords:
- storagekd storhelp Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- storagekd.storhelp
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8232284122741acdca96aa8afc541e69981cc35e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819403"
---
# <a name="storagekdstorhelp"></a>!storagekd.storhelp


**！ Storagekd storhelp** 扩展显示 Storagekd.dll 扩展命令的帮助文本。

```dbgcmd
!storagekd.storhelp 
```

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 8 及更高版本</strong></p></td>
<td align="left"><p>Storagekd.dll</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

下面是 **！ storhelp** 显示的示例 storagekd：

**0： kd &gt; ！ storagekd. storhelp**

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

 

 





