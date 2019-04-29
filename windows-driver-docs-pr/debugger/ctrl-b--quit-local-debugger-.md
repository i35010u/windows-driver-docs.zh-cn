---
title: CTRL+B（退出本地调试器）
description: CTRL + B 密钥会导致调试器突然终止。 这不会结束远程调试会话。
ms.assetid: f70f4c40-244f-4abf-982f-d738800ac621
keywords:
- CTRL + B （Quit 本地调试器） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- CTRL+B (Quit Local Debugger)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9fa104f8e74e3cbf1e6caf6580588f09d9586ea0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374967"
---
# <a name="ctrlb-quit-local-debugger"></a>CTRL+B（退出本地调试器）


CTRL + B 密钥会导致调试器突然终止。 这不会结束远程调试会话。

```dbgcmd
CTRL+B  ENTER 
```

## <span id="ddk_meta_ctrl_b_dbg"></span><span id="DDK_META_CTRL_B_DBG"></span>


### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>调试器</strong></p></td>
<td align="left"><p>CDB 和 KD 仅</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>用户模式下，内核模式</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时、 崩溃转储</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

在 CDB [ **q (Quit)** ](q--qq--quit-.md)用于退出命令。 如果调试器未响应，则只应使用 CTRL + B。

在 KD， **q**命令将结束调试会话并使目标计算机已锁定。 如果你需要保留调试会话 （因此，新的调试程序可以连接到它），或如果您需要使目标计算机运行，则应使用 CTRL + B。

在 WinDbg 中，等效的命令是[文件 |退出](file---exit.md)或 ALT + F4。

 

 





