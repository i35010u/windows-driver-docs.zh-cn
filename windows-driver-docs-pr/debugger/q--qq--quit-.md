---
title: q、qq（退出）
description: 问答命令结束调试会话。
keywords:
- 问： qq (Quit) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- q, qq (Quit)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c008a50ebac80233b1ee82a3a9d7e8dd3c0d8bd6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839799"
---
# <a name="q-qq-quit"></a>q、qq（退出）


**问答****命令结束** 调试会话。  (在 CDB 和 KD 中，此命令也会退出调试器本身。 在 WinDbg 中，此命令将调试器返回到休眠模式。 ) 

```dbgcmd
q 
qq 
```

## <span id="ddk_cmd_quit_dbg"></span><span id="DDK_CMD_QUIT_DBG"></span>


### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>用户模式，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时，故障转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

在用户模式调试中， **q** 命令结束调试会话并关闭目标应用程序。

在内核模式调试中， **q** 命令保存日志文件并结束调试会话。 目标计算机保持锁定状态。

如果此命令在 KD 中不起作用，请在调试器键盘上按 [**CTRL + R + enter**](ctrl-r--re-synchronize-.md) ，然后重试 **q** 命令。 如果此操作不起作用，则必须使用 CTRL + B + ENTER 退出调试器。

**Qq** 命令的行为与 **q** 命令完全相同，除非执行远程调试。 在远程调试过程中， **q** 命令不起作用，但 **qq** 命令会结束调试服务器。 有关此效果的详细信息，请参阅 [通过调试器进行远程调试](remote-debugging-through-the-debugger.md)。

 

 





