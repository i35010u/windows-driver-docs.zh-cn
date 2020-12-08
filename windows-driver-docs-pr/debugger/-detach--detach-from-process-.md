---
title: .detach（从进程分离）
description: Detach 命令结束调试会话，但使任何用户模式目标应用程序都处于运行状态。
keywords:
- 。分离 (从进程分离) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .detach (Detach from Process)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 85274a252e71ebcf78a0ab5146683fc1ebe17c5d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814673"
---
# <a name="detach-detach-from-process"></a>.detach（从进程分离）


**Detach** 命令结束调试会话，但使任何用户模式目标应用程序都处于运行状态。

```dbgcmd
.detach [ /h | /n ]
```

## <a name="span-idddk_meta_detach_from_process_dbgspanspan-idddk_meta_detach_from_process_dbgspanparameters"></a><span id="ddk_meta_detach_from_process_dbg"></span><span id="DDK_META_DETACH_FROM_PROCESS_DBG"></span>参数


<span id="________h______"></span><span id="________H______"></span>**/h**   
任何未完成的调试事件都将继续并标记为已处理。 这是默认值。

<span id="________n______"></span><span id="________N______"></span>**/n**   
任何未完成的调试事件都将继续，而不会标记为已处理。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

对于实时用户模式调试，此命令仅在 Windows XP 和更高版本的 Windows 中受支持。

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
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

此命令将在以下任何情况下结束调试会话：

-   调试用户模式或内核模式转储文件时。

-   调试实时用户模式目标时。

-   Noninvasively 调试用户模式目标时。

如果只调试单个目标，则调试器将在分离后返回到休眠模式。

如果正在 [调试多个目标](debugging-multiple-targets.md)，则调试会话将继续处理剩余的目标。

 

 





