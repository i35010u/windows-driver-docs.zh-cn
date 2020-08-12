---
title: cpuid
description: Cpuid 扩展显示有关系统上的处理器的信息。
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
ms.openlocfilehash: 2bb5d09875a5b2c95d311d3c88b90e78d4c6fe01
ms.sourcegitcommit: bb3b62a57ba3aea4a0adeefd2d81993367b7b334
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "88148425"
---
# <a name="cpuid"></a>!cpuid


**！ Cpuid**扩展显示有关系统上的处理器的信息。

```dbgsyntax
!cpuid [Processor]
```

## <a name="span-idddk__cpuid_dbgspanspan-idddk__cpuid_dbgspanparameters"></a><span id="ddk__cpuid_dbg"></span><span id="DDK__CPUID_DBG"></span>参数


<span id="_______Processor______"></span><span id="_______processor______"></span><span id="_______PROCESSOR______"></span>*处理器*   
指定将显示其信息的处理器。 如果省略此参数，则显示所有处理器。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

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
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Ext.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关如何调试多处理器计算机的详细信息，请参阅[多处理器语法](multiprocessor-syntax.md)。

<a name="remarks"></a>备注
-------

**！ Cpuid**扩展在实时用户模式或内核模式调试、本地内核调试和转储文件调试期间有效。 但是，用户模式小型转储文件只包含有关活动处理器的信息。

如果在用户模式下进行调试，则 **！ cpuid**扩展会描述正在运行目标应用程序的计算机。 在内核模式下，它描述目标计算机。

下面的示例演示了此扩展。

```dbgcmd
kd> !cpuid 
CP  F/M/S  Manufacturer        MHz 
 0  6,5,1  GenuineIntel        700 
 1  8,1,5  AuthenticAMD        700 
```

**CP**列提供处理器号。  (这些数字始终是连续的，从零开始) 。 **制造商**列指定处理器制造商。 " **MHz** " 列指定处理器速度（如果可用）。

对于基于 x86 的处理器或基于 x64 的处理器， **F**列显示处理器家族号， **M**列显示处理器型号， **S**列显示单步大小。


