---
title: .abandon（丢弃进程）
description: 弃用命令结束调试会话，但使目标应用程序处于调试状态。 这会将调试器返回到休眠模式。
keywords:
- 。 (放弃) Windows 调试的进程
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- .abandon (Abandon Process)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b55a9cd083ece4dc345a995de3e2106d4d7450f4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800177"
---
# <a name="abandon-abandon-process"></a>.abandon（丢弃进程）


**弃用** 命令结束调试会话，但使目标应用程序处于调试状态。 这会将调试器返回到休眠模式。

```dbgcmd
.abandon [/h|/n] 
```

## <a name="span-idddk_meta_abandon_process_dbgspanspan-idddk_meta_abandon_process_dbgspanparameters"></a><span id="ddk_meta_abandon_process_dbg"></span><span id="DDK_META_ABANDON_PROCESS_DBG"></span>参数


<span id="________h______"></span><span id="________H______"></span>**/h**   
任何未完成的调试事件都将继续并标记为已处理。 这是默认值。

<span id="________n______"></span><span id="________N______"></span>**/n**   
任何未完成的调试事件都将继续进行处理。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

只有 Windows XP 和更高版本的 Windows 支持此命令。

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
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

如果目标处于调试状态，则可以将新的调试器附加到该目标。 有关详细信息，请参阅 [重新附加到目标应用程序](reattaching-to-the-target-application.md) 。 但是，在放弃一次进程之后，就不能再将其还原到运行状态，而不会附加调试器。

 

 





