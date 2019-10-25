---
title: WdbgExts 内存访问
description: WdbgExts 内存访问
ms.assetid: 7b600d18-343e-4c22-b1e9-5dcc83d88695
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 845b4ca00a6e1a5c9398302422446f7795216e2f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834178"
---
# <a name="wdbgexts-memory-access"></a>WdbgExts 内存访问


本主题简要概述了如何使用 WdbgExts API 执行内存访问。 有关[调试器引擎](introduction.md#debugger-engine)中内存访问的概述，请参阅本文档的[调试器引擎概述](debugger-engine-overview.md)部分中的[内存](memory.md)。

### <a name="span-idvirtual_memoryspanspan-idvirtual_memoryspanvirtual-memory"></a><span id="virtual_memory"></span><span id="VIRTUAL_MEMORY"></span>虚拟内存

可以通过使用[**ReadMemory**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff554287(v=vs.85))函数，并使用[**WriteMemory**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff561420(v=vs.85))函数编写目标的虚拟内存。 可以通过使用[**ReadPointer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-readpointer)、 [**ReadPtr**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-readptr)和[**WritePointer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-writepointer)函数来读取和写入目标的内存中的指针。

若要在虚拟内存中搜索字节模式，请使用[**SearchMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-searchmemory)函数。

[**TranslateVirtualToPhysical**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-translatevirtualtophysical)函数可用于将虚拟内存地址转换为物理内存地址。

[**Disasm**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nc-wdbgexts-pwindbg_disasm)函数可用于在目标上反汇编单个程序集指令。

若要在使用物理地址扩展（PAE）时检查低 4 GB 内存的损坏情况，请使用[**Ioctl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nc-wdbgexts-pwindbg_ioctl_routine)操作[**IG\_LOWMEM\_检查**](https://docs.microsoft.com/previous-versions/ff550931(v=vs.85))。

### <a name="span-idphysical_memoryspanspan-idphysical_memoryspanphysical-memory"></a><span id="physical_memory"></span><span id="PHYSICAL_MEMORY"></span>物理内存

只能在内核模式调试中直接访问物理内存。

可以通过使用[**ReadPhysical**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-readphysical)和[**ReadPhysicalWithFlags**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-readphysicalwithflags)函数来读取目标的物理内存，并使用[**WritePhysical**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-writephysical)和[**WritePhysicalWithFlags**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-writephysicalwithflags)函数编写它们。

若要在物理内存中搜索指向指定范围内的位置的指针，请使用[**Ioctl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nc-wdbgexts-pwindbg_ioctl_routine)操作[**IG\_指针\_搜索\_"物理**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_pointer_search_physical)"。

### <a name="span-idother_data_spacesspanspan-idother_data_spacesspanother-data-spaces"></a><span id="other_data_spaces"></span><span id="OTHER_DATA_SPACES"></span>其他数据空间

在内核模式调试中，除了主内存之外，还可以读取数据和将数据写入到各种数据空间。 可以访问以下数据空间：

<span id="Control-Space_Memory"></span><span id="control-space_memory"></span><span id="CONTROL-SPACE_MEMORY"></span>控制空间内存  
函数[**ReadControlSpace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-readcontrolspace)、 [**ReadControlSpace64**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-readcontrolspace64)、 [**ReadTypedControlSpace32**](https://docs.microsoft.com/previous-versions/ff554339(v=vs.85))和[**ReadTypedControlSpace64**](https://docs.microsoft.com/previous-versions/ff554341(v=vs.85))将读取控制空间中的数据。 [**WriteControlSpace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-writecontrolspace)函数将数据写入控制空间。

<span id="I_O_Memory"></span><span id="i_o_memory"></span><span id="I_O_MEMORY"></span>I/o 内存  
函数[**ReadIoSpace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-readiospace)、 [**ReadIoSpace64**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-readiospace64)、 **ReadIoSpace64**、 [**ReadIoSpaceEx64**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-readiospaceex64)将从系统 i/o 内存和总线 i/o 内存中读取数据。 函数[**WriteIoSpace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-writeiospace)、 [**WriteIoSpace64**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-writeiospace64)、 [**WriteIoSpaceEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-writeiospaceex)和[**WriteIoSpaceEx64**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-writeiospaceex64)会将数据写入系统 i/o 内存和总线 i/o 内存。

<span id="Model_Specific_Register__MSR_"></span><span id="model_specific_register__msr_"></span><span id="MODEL_SPECIFIC_REGISTER__MSR_"></span>模型特定寄存器（MSR）  
函数[**ReadMsr**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-readmsr)和[**WriteMsr**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-writemsr)读取和写入 MSRs。

<span id="System_Bus"></span><span id="system_bus"></span><span id="SYSTEM_BUS"></span>系统总线  
[**Ioctl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nc-wdbgexts-pwindbg_ioctl_routine)操作[**IG\_获取\_总线\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_getsetbusdata)和**IG\_设置\_总线\_数据**读取和写入系统总线数据。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关更强大的内存访问 API，请参阅本文档的[使用调试器引擎 api](using-the-debugger-engine-api.md)中的[内存访问](memory-access.md)部分。

 

 





