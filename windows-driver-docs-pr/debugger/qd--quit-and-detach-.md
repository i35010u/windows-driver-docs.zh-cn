---
title: qd（退出和分离）
description: Qd 命令会结束调试会话，并使任何用户模式目标应用程序处于运行状态。
keywords:
- qd (退出并分离) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- qd (Quit and Detach)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3058aa25bfc3c8c69b95435ef4a9d02e44ff663f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824285"
---
# <a name="qd-quit-and-detach"></a>qd（退出和分离）


**Qd** 命令会结束调试会话，并使任何用户模式目标应用程序处于运行状态。  (在 CDB 和 KD 中，此命令也会退出调试器本身。 在 WinDbg 中，此命令将调试器返回到休眠模式。 ) 

```dbgcmd
qd 
```

## <span id="ddk_cmd_quit_and_detach_dbg"></span><span id="DDK_CMD_QUIT_AND_DETACH_DBG"></span>


### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>仅用户模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>仅限实时调试</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

**Qd** 命令与目标应用程序分离并结束调试会话，并使目标仍在运行。 但是，此命令仅在 Microsoft Windows XP 和更高版本的 Windows 上受支持。 在 Windows 2000 上， **qd** 将生成一条警告消息并且不起作用。

通过调试器执行远程调试时，无法从调试客户端使用 **qd** 命令。

 

 





