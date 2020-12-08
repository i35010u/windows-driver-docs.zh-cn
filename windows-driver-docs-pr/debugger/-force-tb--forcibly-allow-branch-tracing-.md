---
title: .force_tb（强制允许分支跟踪）
description: .Force_tb 命令强制处理器在启动过程的初期跟踪分支。
keywords:
- .force_tb (强制允许分支跟踪) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .force_tb (Forcibly Allow Branch Tracing)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6862564f9051dac316704f00db3286e7d3dae045
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822649"
---
# <a name="force_tb-forcibly-allow-branch-tracing"></a>。强制 \_ tb (强制允许分支跟踪) 


**Force \_ tb** 命令强制处理器在启动过程的初期跟踪分支。

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

通常，在调试器初始化处理器控制块 (PRCB) 后，会启用分支跟踪。 此初始化在启动过程初期发生。

但是，如果在此初始化之前必须使用 [**tb (跟踪到下一个分支)**](tb--trace-to-next-branch-.md) 命令，则可以使用 **. force \_ tb** 命令来启用之前的分支跟踪。 请小心使用此命令，因为它可能会损坏处理器状态。

 

 





