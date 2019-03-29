---
title: cpuid
description: Cpuid 扩展在系统上显示有关的处理器信息。
ms.assetid: 3dbd1079-d129-4e17-8d06-18b25fdd17c9
keywords:
- cpuid Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- cpuid
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e8d14bc7dd929e900aa632359d526087ea96bbc9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577177"
---
# <a name="cpuid"></a>!cpuid


**！ Cpuid**扩展有关的处理器信息显示在系统上。

```dbgsyntax
!cpuid [Processor]
```

## <a name="span-idddkcpuiddbgspanspan-idddkcpuiddbgspanparameters"></a><span id="ddk__cpuid_dbg"></span><span id="DDK__CPUID_DBG"></span>参数


<span id="_______Processor______"></span><span id="_______processor______"></span><span id="_______PROCESSOR______"></span> *Processor*   
指定将显示其信息的处理器。 如果省略此参数，将显示所有处理器。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Ext.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Ext.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关如何调试多处理器计算机的详细信息，请参阅[多处理器语法](multiprocessor-syntax.md)。

<a name="remarks"></a>备注
-------

**！ Cpuid**扩展在实时用户模式或内核模式调试、 本地内核调试，以及调试转储文件的作用。 但是，用户模式的小型转储文件包含仅 active 处理器的信息。

如果在用户模式中进行调试 **！ cpuid**扩展描述运行的目标应用程序的计算机。 在内核模式下，它描述了在目标计算机。

下面的示例显示了此扩展。

```dbgcmd
kd> !cpuid 
CP  F/M/S  Manufacturer        MHz 
 0  6,5,1  GenuineIntel        700 
 1  8,1,5  AuthenticAMD        700 
```

**CP**列给出的处理器数。 （这些数字始终是连续的从零开始）。 **制造商**列指定处理器制造商。 **MHz**列指定的处理器速度，是否可用。

基于 x86 的处理器或基于 x64 的处理器**F**列显示处理器系列号， **M**列将显示的处理器型号，并**S**列会显示单步执行的大小。

对于基于 Itanium 的处理器， **M**列显示的处理器型号时，R 列显示处理器修订号**F**列显示处理器系列数和**一个**列显示的体系结构修订号。

 

 





