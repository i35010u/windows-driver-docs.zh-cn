---
title: .abandon （放弃进程）
description: .Abandon 命令将结束调试会话，但使目标应用程序处于调试状态。 这将返回到休眠模式调试器。
ms.assetid: e44ae9b8-b6a2-4648-911d-61ff3c94527c
keywords:
- .abandon （放弃进程） Windows 调试
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- .abandon (Abandon Process)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f5227a6f1aaa507204ddf470c718241671895f07
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525411"
---
# <a name="abandon-abandon-process"></a>.abandon （放弃进程）


**.Abandon**命令将结束调试会话，但使目标应用程序处于调试状态。 这将返回到休眠模式调试器。

```dbgcmd
.abandon [/h|/n] 
```

## <a name="span-idddkmetaabandonprocessdbgspanspan-idddkmetaabandonprocessdbgspanparameters"></a><span id="ddk_meta_abandon_process_dbg"></span><span id="DDK_META_ABANDON_PROCESS_DBG"></span>参数


<span id="________h______"></span><span id="________H______"></span> **/h**   
将继续并标记为已处理的任何未完成的调试事件。 这是默认设置。

<span id="________n______"></span><span id="________N______"></span> **/n**   
任何未完成的调试事件将继续执行未处理。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

此命令仅支持 Windows XP 和更高版本的 Windows 中。

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

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

如果目标处于调试状态，则新的调试器可以附加到它。 请参阅[重新连接到目标应用程序](reattaching-to-the-target-application.md)有关详细信息。 但是，一次已放弃进程之后，可以永远不会将它还原到运行状态不附加调试器的情况下。

 

 





