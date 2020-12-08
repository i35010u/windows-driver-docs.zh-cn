---
title: cpuinfo
description: Cpuinfo 扩展显示有关目标计算机 CPU 的详细信息。
keywords:
- cpuinfo Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- cpuinfo
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 96a9e2cb19df3c905f2b4d6c64eeee191f05c3ed
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803333"
---
# <a name="cpuinfo"></a>!cpuinfo


**！ Cpuinfo** 扩展显示有关目标计算机 CPU 的详细信息。

语法

```dbgsyntax
!cpuinfo [Processor] 
```

## <a name="span-idddk__cpuinfo_dbgspanspan-idddk__cpuinfo_dbgspanparameters"></a><span id="ddk__cpuinfo_dbg"></span><span id="DDK__CPUINFO_DBG"></span>参数


<span id="_______Processor______"></span><span id="_______processor______"></span><span id="_______PROCESSOR______"></span>*处理器*   
指定要显示的处理器。 如果省略此，则显示所有处理器。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Kdexts.dll

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关调试多处理器计算机的详细信息，请参阅 [多处理器语法](multiprocessor-syntax.md)。

<a name="remarks"></a>备注
-------

执行 [本地内核调试](performing-local-kernel-debugging.md)时，可以使用 **！ cpuinfo** extension 命令。

下面是一个基于 x86 的处理器生成的示例：

```dbgcmd
kd> !cpuinfo
CP F/M/S Manufacturer  MHz Update Signature Features 
 0 6,1,9 GenuineIntel  198 000000d200000000 000000ff 
```

**CP** 列指示处理器数目。 **制造商** 列指定处理器制造商。 " **Mhz** " 或 " **速度** " 列指定处理器的速度（以 MHz 为单位）（如果可用）。

对于基于 x86 的处理器或基于 x64 的处理器， **F** 列显示处理器家族号， **M** 列显示处理器型号， **S** 列显示单步大小。

还将显示其他列，具体取决于计算机的特定体系结构。

有关如何解释每个条目的特定值以及任何其他列的详细信息，请参阅处理器手册。

 

 





