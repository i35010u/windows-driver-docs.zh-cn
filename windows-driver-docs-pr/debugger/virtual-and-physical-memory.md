---
title: 虚拟和物理内存
description: 虚拟和物理内存
ms.assetid: 346a46ea-9d44-4e12-8623-d118cd0c7e25
keywords:
- 内存访问、虚拟内存和物理内存
- 虚拟内存访问
- 物理内存访问
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: c7fff196932c5a0e7040682de66cabb1d273ac79
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89206775"
---
# <a name="virtual-and-physical-memory"></a>虚拟和物理内存


## <span id="ddk_virtual_and_physical_memory_dbx"></span><span id="DDK_VIRTUAL_AND_PHYSICAL_MEMORY_DBX"></span>


引擎提供多种方法用于读取和写入目标的虚拟内存和物理内存。

### <a name="span-idvirtual_memoryspanspan-idvirtual_memoryspanvirtual-memory"></a><span id="virtual_memory"></span><span id="VIRTUAL_MEMORY"></span>虚拟内存

在目标的虚拟内存中指定位置时，将使用目标的虚拟地址空间。 在用户模式调试中，这是当前进程的虚拟地址空间。 在内核模式调试中，这是隐式进程的虚拟地址空间。 有关当前和隐式进程的详细信息，请参阅 [线程和进程](controlling-threads-and-processes.md) 。

目标) 的虚拟内存 (可以使用 [**ReadVirtual**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugdataspaces4-readvirtual) 读取，并使用 [**WriteVirtual**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugdataspaces4-writevirtual)进行编写。

使用便捷的方法 [**ReadPointersVirtual**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugdataspaces4-readpointersvirtual) 和 [**WritePointersVirtual**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugdataspaces4-writepointersvirtual)可以读取和写入目标的内存中的指针。 这些方法将在引擎使用的64位指针与目标使用的本机指针之间自动转换。 请求包含将用于后续请求的指针的内存时，这些方法非常有用，例如，指向字符串的指针。

[**SearchVirtual**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugdataspaces4-searchvirtual)和[**SearchVirtual2**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugdataspaces4-searchvirtual2)方法可用于在目标的虚拟内存中搜索字节模式。

[**FillVirtual**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugdataspaces4-fillvirtual)方法可用于多次将字节模式复制到目标的虚拟内存。

还可以通过使用 [**ReadVirtualUncached**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugdataspaces4-readvirtualuncached) 和 [**WriteVirtualUncached**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugdataspaces4-writevirtualuncached)方法绕过调试器引擎的虚拟内存缓存的方式读取和写入目标的虚拟内存。 这些非缓存版本可用于读取原本不稳定的虚拟内存（如内存映射设备区域），而无需污染或使缓存无效。 未缓存的内存访问只应在需要的情况下使用，因为未缓存访问的性能可能远远低于缓存访问权限。

引擎提供了一些简便方法，可从目标的虚拟内存中读取字符串。 若要从目标读取多字节字符串，请使用 [**ReadMultiByteStringVirtual**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugdataspaces4-readmultibytestringvirtual) 和 [**ReadMultiByteStringVirtualWide**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugdataspaces4-readmultibytestringvirtualwide)。 若要从目标读取 Unicode 字符串，请使用 [**ReadUnicodeStringVirtual**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugdataspaces4-readunicodestringvirtual) 和 [**ReadUnicodeStringVirtualWide**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugdataspaces4-readunicodestringvirtualwide)。

若要查找有关内存位置的信息，请使用 [**GetOffsetInformation**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugdataspaces4-getoffsetinformation)。 并非目标中的所有虚拟地址空间都包含有效的内存。 若要在某个区域中查找有效的内存，请使用 [**GetValidRegionVirtual**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugdataspaces4-getvalidregionvirtual)。 当手动搜索目标中的有效内存时，方法 [**GetNextDifferentlyValidOffsetVirtual**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugdataspaces4-getnextdifferentlyvalidoffsetvirtual) 将会查找下一个可能更改有效性的位置。

### <a name="span-idphysical_memoryspanspan-idphysical_memoryspanphysical-memory"></a><span id="physical_memory"></span><span id="PHYSICAL_MEMORY"></span>物理内存

只能在内核模式调试中直接访问物理内存。

可以通过使用 [**ReadPhysical**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugdataspaces4-readphysical) 和 [**ReadPhysical2**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugdataspaces4-readphysical2)读取目标上的物理内存，并使用 [**WritePhysical**](/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-writephysical) 和 [**WritePhysical2**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugdataspaces4-writephysical2)来编写。

[**FillPhysical**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugdataspaces4-fillphysical)方法可用于多次将字节模式复制到目标的物理内存。

可以使用 [**VirtualToPhysical**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugdataspaces4-virtualtophysical) 方法将目标的虚拟地址空间中的地址转换为目标上的物理地址。 使用 [**GetVirtualTranslationPhysicalOffsets**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugdataspaces4-getvirtualtranslationphysicaloffsets)可以找到用于将虚拟地址转换为物理地址的系统分页结构。

### <a name="span-ideventsspanspan-ideventsspanevents"></a><span id="events"></span><span id="EVENTS"></span>事件

更改目标的虚拟或物理内存时，将调用 [**IDebugEventCallbacks：： ChangeDebuggeeState**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugeventcallbacks-changedebuggeestate) 回调方法。

 

