---
title: qd （Quit 和分离）
description: Qd 命令将结束调试会话，并保持运行任何用户模式目标应用程序。
ms.assetid: 3282c78b-6c4b-4c1b-a086-4890c3140ab9
keywords:
- qd （Quit 和分离） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- qd (Quit and Detach)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c0a1c615d108c8af8319764af5beb651255da28d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523558"
---
# <a name="qd-quit-and-detach"></a>qd （Quit 和分离）


**Qd**命令将结束调试会话，并保持运行任何用户模式目标应用程序。 （在 CDB 和 KD 中，此命令还将退出调试器本身。 在 WinDbg 中，此命令返回调试器到休眠模式。）

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
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>仅限用户模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>仅实时调试</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

**Qd**命令从目标应用程序中分离，并结束调试会话，使目标仍在运行。 但是，仅在 Microsoft Windows XP 和更高版本的 Windows 上支持此命令。 在 Windows 2000 **qd**生成一条警告消息，并不起作用。

当您在执行远程调试通过调试器时，不能使用**qd**命令从调试客户端。

 

 





