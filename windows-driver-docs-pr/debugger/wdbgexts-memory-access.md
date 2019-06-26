---
title: WdbgExts 内存访问
description: WdbgExts 内存访问
ms.assetid: 7b600d18-343e-4c22-b1e9-5dcc83d88695
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d1d934e1916f032bd3186a18a9275163e53dfe7c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369437"
---
# <a name="wdbgexts-memory-access"></a>WdbgExts 内存访问


本主题提供了可以使用 WdbgExts API 执行的内存访问的方式的简要概述。 有关中的内存访问的概述[调试器引擎](introduction.md#debugger-engine)，请参阅[内存](memory.md)中[调试器引擎概述](debugger-engine-overview.md)此文档的部分。

### <a name="span-idvirtualmemoryspanspan-idvirtualmemoryspanvirtual-memory"></a><span id="virtual_memory"></span><span id="VIRTUAL_MEMORY"></span>虚拟内存

可以通过使用读取目标的虚拟内存[ **ReadMemory** ](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff554287(v=vs.85))函数，并使用[ **WriteMemory** ](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff561420(v=vs.85))函数。 可以读取和写入使用中的目标内存的指针[ **ReadPointer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nf-wdbgexts-readpointer)， [ **ReadPtr**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nf-wdbgexts-readptr)，和[ **WritePointer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nf-wdbgexts-writepointer)函数。

若要搜索的字节模式虚拟内存，请使用[ **SearchMemory** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nf-wdbgexts-searchmemory)函数。

[ **TranslateVirtualToPhysical** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nf-wdbgexts-translatevirtualtophysical)函数可用于将虚拟内存地址转换为物理内存地址。

[ **Disasm** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nc-wdbgexts-pwindbg_disasm)函数可用于在目标上的单个程序集指令反汇编。

若要使用的物理地址扩展 (PAE) 时检查较低的 4 GB 的内存已损坏，请使用[ **Ioctl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nc-wdbgexts-pwindbg_ioctl_routine)操作[ **IG\_LOWMEM\_检查**](https://docs.microsoft.com/previous-versions/ff550931(v=vs.85))。

### <a name="span-idphysicalmemoryspanspan-idphysicalmemoryspanphysical-memory"></a><span id="physical_memory"></span><span id="PHYSICAL_MEMORY"></span>物理内存

物理内存只能直接访问在内核模式调试。

可以通过使用读取在目标上的物理内存[ **ReadPhysical** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nf-wdbgexts-readphysical)并[ **ReadPhysicalWithFlags** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nf-wdbgexts-readphysicalwithflags)函数，并写入通过使用[ **WritePhysical** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nf-wdbgexts-writephysical)并[ **WritePhysicalWithFlags** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nf-wdbgexts-writephysicalwithflags)函数。

若要搜索指定的范围内的位置的指针的物理内存，请使用[ **Ioctl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nc-wdbgexts-pwindbg_ioctl_routine)操作[ **IG\_指针\_搜索\_物理**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/ns-wdbgexts-_pointer_search_physical)。

### <a name="span-idotherdataspacesspanspan-idotherdataspacesspanother-data-spaces"></a><span id="other_data_spaces"></span><span id="OTHER_DATA_SPACES"></span>其他数据空间

在内核模式调试，就可以读取和写入到各种数据空间除了主内存的数据。 可以访问以下数据空间：

<span id="Control-Space_Memory"></span><span id="control-space_memory"></span><span id="CONTROL-SPACE_MEMORY"></span>Control-Space Memory  
函数[ **ReadControlSpace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nf-wdbgexts-readcontrolspace)， [ **ReadControlSpace64**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nf-wdbgexts-readcontrolspace64)， [ **ReadTypedControlSpace32**](https://docs.microsoft.com/previous-versions/ff554339(v=vs.85))，并[ **ReadTypedControlSpace64** ](https://docs.microsoft.com/previous-versions/ff554341(v=vs.85))将从控件空间读取数据。 [ **WriteControlSpace** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nf-wdbgexts-writecontrolspace)函数会将数据写入到控制空间。

<span id="I_O_Memory"></span><span id="i_o_memory"></span><span id="I_O_MEMORY"></span>I/O Memory  
函数[ **ReadIoSpace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nf-wdbgexts-readiospace)， [ **ReadIoSpace64**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nf-wdbgexts-readiospace64)， **ReadIoSpace64**， [**ReadIoSpaceEx64** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nf-wdbgexts-readiospaceex64)从系统 I/O： 内存中读取数据并将总线 I/O： 内存。 函数[ **WriteIoSpace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nf-wdbgexts-writeiospace)， [ **WriteIoSpace64**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nf-wdbgexts-writeiospace64)， [ **WriteIoSpaceEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nf-wdbgexts-writeiospaceex)，并[ **WriteIoSpaceEx64** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nf-wdbgexts-writeiospaceex64)将数据写入系统 I/O： 内存和 I/O： 内存总线。

<span id="Model_Specific_Register__MSR_"></span><span id="model_specific_register__msr_"></span><span id="MODEL_SPECIFIC_REGISTER__MSR_"></span>模型特定寄存器 (MSR)  
函数[ **ReadMsr** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nf-wdbgexts-readmsr)并[ **WriteMsr** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nf-wdbgexts-writemsr)读取和写入 MSRs。

<span id="System_Bus"></span><span id="system_bus"></span><span id="SYSTEM_BUS"></span>系统总线  
[ **Ioctl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nc-wdbgexts-pwindbg_ioctl_routine) operations [ **IG\_获取\_总线\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/ns-wdbgexts-_getsetbusdata)和**IG\_设置\_总线\_数据**读取和写入系统总线数据。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

功能更强大内存访问 API，请参阅[内存访问](memory-access.md)中[使用调试器引擎 API](using-the-debugger-engine-api.md)此文档的部分。

 

 





