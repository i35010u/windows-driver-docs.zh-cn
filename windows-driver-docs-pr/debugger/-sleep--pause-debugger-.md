---
title: .sleep （暂停调试器）
description: .Sleep 命令将导致用户模式下调试器以暂停和目标计算机变为活动状态。 当正在控制用户模式下的调试程序与内核调试程序时，仅使用此命令。
ms.assetid: bc3ee17f-e3b8-4bdb-8c80-6b1fef29000e
keywords:
- 暂停调试器 (.sleep) 命令
- 控制用户模式下的调试程序与内核调试器，暂停调试器 (.sleep) 命令
- .sleep （暂停调试器） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .sleep (Pause Debugger)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1d05c72238575ddf79a51f0f7e9f2035212e0dde
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554927"
---
# <a name="sleep-pause-debugger"></a>.sleep （暂停调试器）


**.Sleep**命令将导致用户模式下的调试器暂停和目标计算机变为活动状态。 当正在控制用户模式下的调试程序与内核调试程序时，仅使用此命令。

```dbgcmd
.sleep milliseconds
```

## <a name="span-idddkmetapausedebuggerdbgspanspan-idddkmetapausedebuggerdbgspanparameters"></a><span id="ddk_meta_pause_debugger_dbg"></span><span id="DDK_META_PAUSE_DEBUGGER_DBG"></span>参数


<span id="_______milliseconds______"></span><span id="_______MILLISECONDS______"></span> *milliseconds*   
指定暂停，以毫秒为单位的长度。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>控制用户模式下的调试程序与内核调试程序</p></td>
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

有关详细信息和有关如何唤醒处于睡眠模式下调试程序的信息，请参阅[控制用户模式下调试程序与内核调试程序](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)。

<a name="remarks"></a>备注
-------

当正在控制用户模式下的调试程序与内核调试程序，并显示在内核调试程序用户模式下调试器提示符下时，此命令将激活睡眠模式。 内核调试程序、 用户模式下调试程序，而且目标应用程序将所有被冻结，但成为活动部署的目标计算机的其余部分。

如果在任何其他方案中使用此命令，它只需将冻结一段时间内的调试器。

睡眠时间以毫秒为单位和解释根据默认基数，除非如前缀**0n**使用。 因此，如果默认基数为 16，以下命令将导致为进入睡眠状态的 65 秒：

```dbgcmd
0:000> .sleep 10000
```

 

 





