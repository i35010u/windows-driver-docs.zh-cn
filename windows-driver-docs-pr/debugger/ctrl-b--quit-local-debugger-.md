---
title: CTRL+B（退出本地调试器）
description: CTRL + B 键会使调试器突然终止。 这不会结束远程调试会话。
keywords:
- CTRL + B (退出本地调试器) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- CTRL+B (Quit Local Debugger)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 108cfe0b1d2b279d54f262f221fe828981287941
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96787011"
---
# <a name="ctrlb-quit-local-debugger"></a>CTRL+B（退出本地调试器）


CTRL + B 键会使调试器突然终止。 这不会结束远程调试会话。

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
<td align="left"><p>仅限 CDB 和 KD</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>用户模式，内核模式</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时，故障转储</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

在 CDB 中， [**q (Quit)**](q--qq--quit-.md) 命令退出。 仅当调试器没有响应时，才应使用 CTRL + B。

在 KD 中， **q** 命令会结束调试会话，并使目标计算机保持锁定状态。 如果需要保留调试会话 (以便新的调试器可以连接到该会话) ，或者，如果需要使目标计算机保持运行，则应使用 CTRL + B。

在 WinDbg 中，等效命令为 [File |退出](file---exit.md) 或按 ALT + F4。

 

 





