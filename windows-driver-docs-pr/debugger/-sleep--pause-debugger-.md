---
title: .sleep（暂停调试器）
description: Sleep 命令使用户模式调试器暂停，并使目标计算机变为活动状态。 仅当从内核调试器控制用户模式调试器时才使用此命令。
keywords:
- " ( 休眠) 命令暂停调试器"
- 从内核调试器控制用户模式调试器，暂停调试器 ( 休眠) 命令
- 。睡眠 (在 Windows 调试) 暂停调试器
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .sleep (Pause Debugger)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 476c51eb92bce764148157be3d5a1f2bfabc549f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799855"
---
# <a name="sleep-pause-debugger"></a>.sleep（暂停调试器）


**Sleep** 命令使用户模式调试器暂停，并使目标计算机变为活动状态。 仅当从内核调试器控制用户模式调试器时才使用此命令。

```dbgcmd
.sleep milliseconds
```

## <a name="span-idddk_meta_pause_debugger_dbgspanspan-idddk_meta_pause_debugger_dbgspanparameters"></a><span id="ddk_meta_pause_debugger_dbg"></span><span id="DDK_META_PAUSE_DEBUGGER_DBG"></span>参数


<span id="_______milliseconds______"></span><span id="_______MILLISECONDS______"></span>*毫秒*   
指定暂停的长度（以毫秒为单位）。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>从内核调试器控制用户模式调试器</p></td>
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

有关如何在睡眠模式下唤醒调试器的详细信息和信息，请参阅 [从内核调试器控制 User-Mode 调试器](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)。

<a name="remarks"></a>备注
-------

当你从内核调试器控制用户模式调试器，并且用户模式调试器提示在内核调试器中可见时，此命令将激活休眠模式。 内核调试器、用户模式调试器和目标应用程序都将冻结，但目标计算机的其余部分将变为活动状态。

如果在任何其他情况下使用此命令，它将只是在一段时间内冻结调试器。

睡眠时间以毫秒为单位，并按默认基数解释，除非使用诸如 **0n** 的前缀。 因此，如果默认基数为16，则以下命令将导致大约65秒的睡眠：

```dbgcmd
0:000> .sleep 10000
```

 

 





