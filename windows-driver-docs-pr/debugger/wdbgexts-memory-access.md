---
title: WdbgExts 内存访问
description: WdbgExts 内存访问
ms.assetid: 7b600d18-343e-4c22-b1e9-5dcc83d88695
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c51b1297822e443bd1b93ae9f00f62a591194f20
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325835"
---
# <a name="wdbgexts-memory-access"></a>WdbgExts 内存访问


本主题提供了可以使用 WdbgExts API 执行的内存访问的方式的简要概述。 有关中的内存访问的概述[调试器引擎](introduction.md#debugger-engine)，请参阅[内存](memory.md)中[调试器引擎概述](debugger-engine-overview.md)此文档的部分。

### <a name="span-idvirtualmemoryspanspan-idvirtualmemoryspanvirtual-memory"></a><span id="virtual_memory"></span><span id="VIRTUAL_MEMORY"></span>虚拟内存

可以通过使用读取目标的虚拟内存[ **ReadMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff554287)函数，并使用[ **WriteMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff561420)函数。 可以读取和写入使用中的目标内存的指针[ **ReadPointer**](https://msdn.microsoft.com/library/windows/hardware/ff554318)， [ **ReadPtr**](https://msdn.microsoft.com/library/windows/hardware/ff554330)，和[ **WritePointer** ](https://msdn.microsoft.com/library/windows/hardware/ff561450)函数。

若要搜索的字节模式虚拟内存，请使用[ **SearchMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff554742)函数。

[ **TranslateVirtualToPhysical** ](https://msdn.microsoft.com/library/windows/hardware/ff558914)函数可用于将虚拟内存地址转换为物理内存地址。

[ **Disasm** ](https://msdn.microsoft.com/library/windows/hardware/ff541945)函数可用于在目标上的单个程序集指令反汇编。

若要使用的物理地址扩展 (PAE) 时检查较低的 4 GB 的内存已损坏，请使用[ **Ioctl** ](https://msdn.microsoft.com/library/windows/hardware/ff551084)操作[ **IG\_LOWMEM\_检查**](https://msdn.microsoft.com/library/windows/hardware/ff550931)。

### <a name="span-idphysicalmemoryspanspan-idphysicalmemoryspanphysical-memory"></a><span id="physical_memory"></span><span id="PHYSICAL_MEMORY"></span>物理内存

物理内存只能直接访问在内核模式调试。

可以通过使用读取在目标上的物理内存[ **ReadPhysical** ](https://msdn.microsoft.com/library/windows/hardware/ff554310)并[ **ReadPhysicalWithFlags** ](https://msdn.microsoft.com/library/windows/hardware/ff554315)函数，并写入通过使用[ **WritePhysical** ](https://msdn.microsoft.com/library/windows/hardware/ff561432)并[ **WritePhysicalWithFlags** ](https://msdn.microsoft.com/library/windows/hardware/ff561448)函数。

若要搜索指定的范围内的位置的指针的物理内存，请使用[ **Ioctl** ](https://msdn.microsoft.com/library/windows/hardware/ff551084)操作[ **IG\_指针\_搜索\_物理**](https://msdn.microsoft.com/library/windows/hardware/ff550935)。

### <a name="span-idotherdataspacesspanspan-idotherdataspacesspanother-data-spaces"></a><span id="other_data_spaces"></span><span id="OTHER_DATA_SPACES"></span>其他数据空间

在内核模式调试，就可以读取和写入到各种数据空间除了主内存的数据。 可以访问以下数据空间：

<span id="Control-Space_Memory"></span><span id="control-space_memory"></span><span id="CONTROL-SPACE_MEMORY"></span>Control-Space Memory  
函数[ **ReadControlSpace**](https://msdn.microsoft.com/library/windows/hardware/ff553527)， [ **ReadControlSpace64**](https://msdn.microsoft.com/library/windows/hardware/ff553532)， [ **ReadTypedControlSpace32**](https://msdn.microsoft.com/library/windows/hardware/ff554339)，并[ **ReadTypedControlSpace64** ](https://msdn.microsoft.com/library/windows/hardware/ff554341)将从控件空间读取数据。 [ **WriteControlSpace** ](https://msdn.microsoft.com/library/windows/hardware/ff561375)函数会将数据写入到控制空间。

<span id="I_O_Memory"></span><span id="i_o_memory"></span><span id="I_O_MEMORY"></span>I/O Memory  
函数[ **ReadIoSpace**](https://msdn.microsoft.com/library/windows/hardware/ff553574)， [ **ReadIoSpace64**](https://msdn.microsoft.com/library/windows/hardware/ff553577)， **ReadIoSpace64**， [**ReadIoSpaceEx64** ](https://msdn.microsoft.com/library/windows/hardware/ff553583)从系统 I/O： 内存中读取数据并将总线 I/O： 内存。 函数[ **WriteIoSpace**](https://msdn.microsoft.com/library/windows/hardware/ff561406)， [ **WriteIoSpace64**](https://msdn.microsoft.com/library/windows/hardware/ff561408)， [ **WriteIoSpaceEx** ](https://msdn.microsoft.com/library/windows/hardware/ff561413)，并[ **WriteIoSpaceEx64** ](https://msdn.microsoft.com/library/windows/hardware/ff561414)将数据写入系统 I/O： 内存和 I/O： 内存总线。

<span id="Model_Specific_Register__MSR_"></span><span id="model_specific_register__msr_"></span><span id="MODEL_SPECIFIC_REGISTER__MSR_"></span>模型特定寄存器 (MSR)  
函数[ **ReadMsr** ](https://msdn.microsoft.com/library/windows/hardware/ff554289)并[ **WriteMsr** ](https://msdn.microsoft.com/library/windows/hardware/ff561424)读取和写入 MSRs。

<span id="System_Bus"></span><span id="system_bus"></span><span id="SYSTEM_BUS"></span>系统总线  
[ **Ioctl** ](https://msdn.microsoft.com/library/windows/hardware/ff551084) operations [ **IG\_获取\_总线\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff550913)和**IG\_设置\_总线\_数据**读取和写入系统总线数据。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

功能更强大内存访问 API，请参阅[内存访问](memory-access.md)中[使用调试器引擎 API](using-the-debugger-engine-api.md)此文档的部分。

 

 





