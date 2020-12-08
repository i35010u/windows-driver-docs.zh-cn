---
title: symsrv 扩展命令
description: Symsrv 扩展关闭符号服务器客户端。
keywords:
- symsrv Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- symsrv
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1baeb3d71ed6c014cafeddc9b099982bc37e50c8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830321"
---
# <a name="symsrv"></a>!symsrv


**！ Symsrv** extension 关闭符号服务器客户端。

```dbgcmd
!symsrv close
```

## <span id="ddk__symsrv_dbg"></span><span id="DDK__SYMSRV_DBG"></span>


### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Dbghelp.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Dbghelp.dll</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

**！ Symsrv close** extension 将关闭任何活动的符号服务器客户端。

如果需要重新同步连接，这会很有用。

如果你之前拒绝了 internet 身份验证请求，则需要使用 **！ symsrv close** 重新连接到符号存储区。 有关详细信息，请参阅 [防火墙和代理服务器](firewalls-and-proxy-servers.md) 。

 

 





