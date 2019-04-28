---
title: cpuinfo
description: Cpuinfo 扩展显示有关目标计算机的 CPU 的详细的信息。
ms.assetid: 1e7c348b-0de8-4925-b0a9-300391b6064e
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
ms.openlocfilehash: 08183c39fdce0fd111eec941df723c6d5376bd12
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334602"
---
# <a name="cpuinfo"></a>!cpuinfo


**！ Cpuinfo**扩展显示有关目标计算机的 CPU 详细的信息。

语法

```dbgsyntax
!cpuinfo [Processor] 
```

## <a name="span-idddkcpuinfodbgspanspan-idddkcpuinfodbgspanparameters"></a><span id="ddk__cpuinfo_dbg"></span><span id="DDK__CPUINFO_DBG"></span>参数


<span id="_______Processor______"></span><span id="_______processor______"></span><span id="_______PROCESSOR______"></span> *Processor*   
指定要显示的处理器。 如果省略此属性，将显示所有处理器。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Kdexts.dll

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关调试多处理器计算机的详细信息，请参阅[多处理器语法](multiprocessor-syntax.md)。

<a name="remarks"></a>备注
-------

**！ Cpuinfo**执行时，可以使用扩展命令[本地内核调试](performing-local-kernel-debugging.md)。

下面是基于 x86 的处理器生成示例：

```dbgcmd
kd> !cpuinfo
CP F/M/S Manufacturer  MHz Update Signature Features 
 0 6,1,9 GenuineIntel  198 000000d200000000 000000ff 
```

下面是用于基于 Itanium 处理器生成示例：

```dbgcmd
kd> !cpuinfo
CP M/R/F/A Manufacturer     SerialNumber     Features         Speed
 0 2,1,31,0 GenuineIntel     0000000000000000 0000000000000001 1300 Mhz
 1 2,1,31,0 GenuineIntel     0000000000000000 0000000000000001 1300 Mhz
```

**CP**列指示处理器数。 **制造商**列指定处理器制造商。 **MHz**或**速度**列指定 MHz 的处理器的速度，是否可用。

基于 x86 的处理器或基于 x64 的处理器**F**列显示处理器系列号， **M**列将显示的处理器型号，并**S**列会显示单步执行的大小。

对于基于 Itanium 的处理器， **M**列显示处理器型号**R**列将显示处理器修订号**F**列显示处理器系列号，并**A**列显示的体系结构修订号。

其他列也会显示，具体取决于计算机的特定体系结构。

有关如何解释每个条目，以及任何其他列的特定值的详细信息，请查阅处理器手册。

 

 





