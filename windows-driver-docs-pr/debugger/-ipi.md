---
title: ipi
description: Ipi 扩展显示指定的处理器的 interprocessor 中断 (IPI) 状态。
ms.assetid: 2727d429-82f5-44a6-943b-0a3f2d3385a3
keywords:
- IPI （interprocessor 中断）
- ipi Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ipi
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 44ebc77341bacc9f3a67a9fe968686c835d1a6b0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533204"
---
# <a name="ipi"></a>!ipi


**！ Ipi**扩展显示指定处理器 interprocessor 中断 (IPI) 的状态。

```dbgcmd
!ipi [Processor]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Processor______"></span><span id="_______processor______"></span><span id="_______PROCESSOR______"></span> *Processor*   
指定一个处理器。 如果*处理器*是省略，将显示每个处理器的 IPI 状态。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>不可用</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

此扩展命令仅用于基于 x86 的目标计算机。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

Ipi 有关的信息，请参阅*Microsoft Windows Internals*由 Mark Russinovich 和 David solomon 合著。

<a name="remarks"></a>备注
-------

下面是输出的来自此扩展插件示例：

```dbgcmd
0: kd> !ipi
IPI State for Processor 0
  Worker Routine:  nt!KiFlushTargetMultipleTb [Stale]
  Parameter[0]:    0
  Parameter[1]:    3
  Parameter[2]:    F7C98770
  Ipi Trap Frame:  F7CCCCDC [.trap F7CCCCDC]
  Signal Done:     0
  IPI Frozen:      24 [FreezeActive] [Owner]
  Request Summary: 0
  Target Set:      0
  Packet Barrier:  0

IPI State for Processor 1
  Worker Routine:  nt!KiFlushTargetMultipleTb [Stale]
  Parameter[0]:    1
  Parameter[1]:    3
  Parameter[2]:    F7CDCD28
  Ipi Trap Frame:  F7C8CCC4 [.trap F7C8CCC4]
  Signal Done:     0
  IPI Frozen:      2 [Frozen]
  Request Summary: 0
  Target Set:      0
  Packet Barrier:  0
```

 

 





