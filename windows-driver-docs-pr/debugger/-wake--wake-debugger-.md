---
title: .wake（唤醒调试器）
description: .Wake 命令会使睡眠模式下，若要结束。 仅当正在控制用户模式下的调试程序与内核调试程序时，才使用此命令。
ms.assetid: 01aead7e-1f46-46cf-a697-ab5ff6329ac7
keywords:
- 唤醒调试器 (.wake) 命令
- 控制用户模式下的调试程序与内核调试器，唤醒调试器 (.wake) 命令
- .wake （唤醒调试器） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .wake (Wake Debugger)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 30ae68fce209bb88acec21b488ebf8d053e76589
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341781"
---
# <a name="wake-wake-debugger"></a>.wake（唤醒调试器）


**.Wake**原因睡眠模式下，若要结束的命令。 仅当正在控制用户模式下的调试程序与内核调试程序时，才使用此命令。

```dbgcmd
.wake PID
```

## <a name="span-idddkmetawakedebuggerdbgspanspan-idddkmetawakedebuggerdbgspanparameters"></a><span id="ddk_meta_wake_debugger_dbg"></span><span id="DDK_META_WAKE_DEBUGGER_DBG"></span>参数


<span id="_______PID______"></span><span id="_______pid______"></span> *PID*   
用户模式下调试程序的进程 ID。

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

有关更多详细信息，请参阅[控制用户模式下调试程序与内核调试程序](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)。 有关如何查找调试器的进程 ID 的信息，请参阅[查找进程 ID](finding-the-process-id.md)。

<a name="remarks"></a>备注
-------

当您控制用户模式下的调试程序与内核调试程序和系统处于睡眠模式下时，此命令可以用于唤醒调试器在睡眠计时器用完之前。

在目标计算机上的用户模式下调试器也不在主机上的内核调试器，不会发出此命令。 它必须从第三个调试程序 （KD、 CDB 或 NTSD） 颁发在目标计算机上运行。

此调试器可以为此，明确启动，也可以是碰巧运行的另一个调试器。 但是，如果已在运行的任何其他调试器，它容易只是为了使用与 CDB **-唤醒** [**命令行选项**](cdb-command-line-options.md)。

 

 





