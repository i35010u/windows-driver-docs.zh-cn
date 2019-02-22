---
title: .force_tb （强制允许分支跟踪）
description: .Force_tb 命令会强制在启动过程中尽早跟踪分支到处理器。
ms.assetid: ac4aabfa-6d00-4478-9c13-213bf89f613a
keywords:
- .force_tb （强制允许分支跟踪） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .force_tb (Forcibly Allow Branch Tracing)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9ec13cd9f4e87654e952746a81d5e4df6b3f282c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523343"
---
# <a name="forcetb-forcibly-allow-branch-tracing"></a>.force\_tb （强制允许分支跟踪）


**.Force\_tb**命令会强制在启动过程中尽早跟踪分支到处理器。

```dbgcmd
.force_tb 
```

## <span id="ddk_meta_forcibly_allow_branch_tracing_dbg"></span><span id="DDK_META_FORCIBLY_ALLOW_BRANCH_TRACING_DBG"></span>


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

通常情况下，调试器初始化处理器控制块 (PRCB) 后启用分支跟踪。 在启动过程中尽早将发生此初始化。

但是，如果您必须使用[ **tb （跟踪到下一个分支）** ](tb--trace-to-next-branch-.md)命令之前此初始化，可以使用 **.force\_tb**命令以启用分支跟踪前面。 请谨慎使用此命令，因为它可能会损坏处理器状态。

 

 





