---
title: 问： qq （退出）
description: '问: 和 qq 命令结束调试会话。'
ms.assetid: 94d35997-8b21-4d25-b2ae-4b2a78240153
keywords:
- 问:、 qq (Quit) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- q, qq (Quit)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1bfe9421c9da02d26bbbc58b3794de108c53093e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542251"
---
# <a name="q-qq-quit"></a>问： qq （退出）


**Q**并**qq**命令结束调试会话。 （在 CDB 和 KD 中，此命令还将退出调试器本身。 在 WinDbg 中，此命令返回调试器到休眠模式。）

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
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>用户模式下，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时、 崩溃转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

在用户模式下调试中， **q**命令将结束调试会话并关闭目标应用程序。

在内核模式调试中， **q**命令将保存日志文件，并结束调试会话。 目标计算机保持锁定状态。

如果在 KD 中时，此命令不起作用，请按[ **CTRL + R + ENTER** ](ctrl-r--re-synchronize-.md)上调试器键盘，然后重试**q**命令。 如果此操作不起作用，则必须使用 CTRL + B + ENTER 以退出调试器。

**Qq**命令的行为完全相同**q**命令，除非您正在执行远程调试。 在远程调试期间**q**命令不起作用，但**qq**命令将结束调试服务器。 有关这种效果的详细信息，请参阅[远程调试通过调试器](remote-debugging-through-the-debugger.md)。

 

 





