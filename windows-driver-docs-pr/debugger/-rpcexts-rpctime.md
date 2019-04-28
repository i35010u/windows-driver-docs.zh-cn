---
title: rpcexts.rpctime
description: Rpcexts.rpctime 扩展显示的当前系统时间。
ms.assetid: 72d54357-6b16-4d53-9909-ba201bb33519
keywords:
- rpcexts.rpctime Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- rpcexts.rpctime
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 645a9c477d60059a22228fdff7f153f0d9a14ae6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335783"
---
# <a name="rpcextsrpctime"></a>!rpcexts.rpctime


**！ Rpcexts.rpctime**扩展显示的当前系统时间。

```dbgcmd
!rpcexts.rpctime 
```

## <span id="ddk__rpcexts_rpctime_dbg"></span><span id="DDK__RPCEXTS_RPCTIME_DBG"></span>


### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Rpcexts.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Rpcexts.dll</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

与 CDB 或用户模式下 WinDbg，则仅可以使用此扩展。

下面是一个示例：

```dbgcmd
0:001> !rpcexts.rpctime
Current time is: 059931.126  (0x00ea1b.07e)
```

 

 





