---
title: .wake（唤醒调试器）
description: 唤醒命令使睡眠模式结束。 仅当从内核调试器控制用户模式调试器时才使用此命令。
keywords:
- 唤醒) 命令 ( 唤醒调试器
- 从内核调试器、唤醒调试器 ( 唤醒) 命令控制用户模式调试器
- 。唤醒 (唤醒调试器) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .wake (Wake Debugger)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 336014a48702a594b5a66731c9d018647398bbf7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838693"
---
# <a name="wake-wake-debugger"></a>.wake（唤醒调试器）


**唤醒** 命令使睡眠模式结束。 仅当从内核调试器控制用户模式调试器时才使用此命令。

```dbgcmd
.wake PID
```

## <a name="span-idddk_meta_wake_debugger_dbgspanspan-idddk_meta_wake_debugger_dbgspanparameters"></a><span id="ddk_meta_wake_debugger_dbg"></span><span id="DDK_META_WAKE_DEBUGGER_DBG"></span>参数


<span id="_______PID______"></span><span id="_______pid______"></span>*PID*   
用户模式调试器的进程 ID。

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

有关更多详细信息，请参阅 [从内核调试器控制 User-Mode 调试器](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)。 有关如何查找调试器的进程 ID 的信息，请参阅 [查找进程 id](finding-the-process-id.md)。

<a name="remarks"></a>备注
-------

当你从内核调试器控制用户模式调试器并且系统处于休眠模式时，此命令可用于在睡眠计时器运行之前唤醒调试器。

此命令不在目标计算机上的用户模式调试器中，也不会在主机上的内核调试器中发出。 它必须从在目标计算机上运行的第三个调试器 (KD、CDB 或 NTSD) 发出。

此调试器可以专门用于此目的，也可以是正在运行的另一个调试器。 但是，如果没有其他调试器正在运行，只需使用包含 **-唤醒**[**命令行选项**](cdb-command-line-options.md)的 CDB 即可。

 

 





