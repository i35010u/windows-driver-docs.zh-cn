---
title: rpcexts.rpctime
description: Rpcexts. rpctime 扩展显示当前系统时间。
keywords:
- rpcexts rpctime Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- rpcexts.rpctime
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: cc5b04ed0aaddd9fe665b72148a3069409d7ddf0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820993"
---
# <a name="rpcextsrpctime"></a>!rpcexts.rpctime


**！ Rpcexts rpctime** 扩展显示当前系统时间。

```dbgcmd
!rpcexts.rpctime 
```

## <span id="ddk__rpcexts_rpctime_dbg"></span><span id="DDK__RPCEXTS_RPCTIME_DBG"></span>


### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

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

此扩展只能与 CDB 一起使用，也可与用户模式 WinDbg 一起使用。

以下是示例：

```dbgcmd
0:001> !rpcexts.rpctime
Current time is: 059931.126  (0x00ea1b.07e)
```

 

 





