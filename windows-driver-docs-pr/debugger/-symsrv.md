---
title: symsrv 扩展命令
description: Symsrv 扩展关闭符号服务器客户端。
ms.assetid: 666fa9d7-f723-4745-95fc-17aa20993b42
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
ms.openlocfilehash: 329178bf873560d7064569d0c5148f2c0d4770fb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334210"
---
# <a name="symsrv"></a>!symsrv


**！ Symsrv**扩展关闭符号服务器客户端。

```dbgcmd
!symsrv close
```

## <span id="ddk__symsrv_dbg"></span><span id="DDK__SYMSRV_DBG"></span>


### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

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

**！ Symsrv 关闭**扩展将会关闭任何活动的符号服务器客户端。

这很有用，如果你需要重新同步你的连接。

如果以前已被拒绝的 internet 身份验证请求，你将需要使用 **！ symsrv 关闭**重新连接到符号存储区。 请参阅[防火墙和代理服务器](firewalls-and-proxy-servers.md)有关详细信息。

 

 





