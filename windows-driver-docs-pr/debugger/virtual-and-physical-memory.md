---
title: 虚拟和物理内存
description: 虚拟和物理内存
ms.assetid: 346a46ea-9d44-4e12-8623-d118cd0c7e25
keywords:
- 内存访问，虚拟和物理内存
- 虚拟内存访问
- 物理内存访问
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: e134b53e280f31c671ae02adadd0b650d2d8dc40
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325908"
---
# <a name="virtual-and-physical-memory"></a>虚拟和物理内存


## <span id="ddk_virtual_and_physical_memory_dbx"></span><span id="DDK_VIRTUAL_AND_PHYSICAL_MEMORY_DBX"></span>


引擎提供了多种方法来读取和写入目标的虚拟和物理内存。

### <a name="span-idvirtualmemoryspanspan-idvirtualmemoryspanvirtual-memory"></a><span id="virtual_memory"></span><span id="VIRTUAL_MEMORY"></span>虚拟内存

当指定位置的目标虚拟内存中，将使用目标的虚拟地址空间。 在用户模式调试，这是当前进程的虚拟地址空间。 在内核模式调试，这是进程的隐式的虚拟地址空间。 请参阅[线程和进程](controlling-threads-and-processes.md)有关的当前和隐式过程的详细信息。

可以通过使用读取 （目标） 的虚拟内存[ **ReadVirtual** ](https://msdn.microsoft.com/library/windows/hardware/ff554359)并使用编写[ **WriteVirtual**](https://msdn.microsoft.com/library/windows/hardware/ff561468)。

可以读取和写入使用便捷方法中的目标内存的指针[ **ReadPointersVirtual** ](https://msdn.microsoft.com/library/windows/hardware/ff554323)并[ **WritePointersVirtual** ](https://msdn.microsoft.com/library/windows/hardware/ff561451). 这些方法将自动转换引擎使用的 64 位指针和本机指针由目标之间。 请求内存，其中包含将用于后续请求-例如，为字符串的指针的指针时，这些方法非常有用。

[ **SearchVirtual** ](https://msdn.microsoft.com/library/windows/hardware/ff554747)并[ **SearchVirtual2** ](https://msdn.microsoft.com/library/windows/hardware/ff554755)方法可用于搜索目标的虚拟内存的字节模式。

[ **FillVirtual** ](https://msdn.microsoft.com/library/windows/hardware/ff545395)方法可用于将一种模式的字节，多个时间复制到目标的虚拟内存。

目标的虚拟内存还可以读取和写入会绕过调试器引擎的虚拟内存缓存使用的方法的方式[ **ReadVirtualUncached** ](https://msdn.microsoft.com/library/windows/hardware/ff554361)和[ **WriteVirtualUncached**](https://msdn.microsoft.com/library/windows/hardware/ff561473)。 这些未缓存的版本可用于读取是本质上是易失性，例如设备内存映射区域，而无需干扰或使缓存失效的虚拟内存。 未缓存的访问应仅用于在情况下时是必需的因为之后未缓存的访问的性能的内存可以显著低于缓存的访问。

引擎提供了一些便捷方法以从目标的虚拟内存读取的字符串。 若要从目标读取多字节字符串，使用[ **ReadMultiByteStringVirtual** ](https://msdn.microsoft.com/library/windows/hardware/ff554300)并[ **ReadMultiByteStringVirtualWide**](https://msdn.microsoft.com/library/windows/hardware/ff554304)。 若要从目标读取 Unicode 字符串，使用[ **ReadUnicodeStringVirtual** ](https://msdn.microsoft.com/library/windows/hardware/ff554351)并[ **ReadUnicodeStringVirtualWide**](https://msdn.microsoft.com/library/windows/hardware/ff554357)。

若要查找有关内存位置的信息，请使用[ **GetOffsetInformation**](https://msdn.microsoft.com/library/windows/hardware/ff548055)。 并非所有目标中的虚拟地址空间包含有效的内存。 若要在区域中查找有效的内存，请使用[ **GetValidRegionVirtual**](https://msdn.microsoft.com/library/windows/hardware/ff549471)。 手动搜索目标，该方法中的有效内存时[ **GetNextDifferentlyValidOffsetVirtual** ](https://msdn.microsoft.com/library/windows/hardware/ff547847)有效性可能会在其中更改下一个位置。

### <a name="span-idphysicalmemoryspanspan-idphysicalmemoryspanphysical-memory"></a><span id="physical_memory"></span><span id="PHYSICAL_MEMORY"></span>物理内存

物理内存只能直接访问在内核模式调试。

可以通过使用读取在目标上的物理内存[ **ReadPhysical** ](https://msdn.microsoft.com/library/windows/hardware/ff554313)并[ **ReadPhysical2**](https://msdn.microsoft.com/library/windows/hardware/ff554311)，并通过使用编写[**WritePhysical** ](https://msdn.microsoft.com/library/windows/hardware/ff561432)并[ **WritePhysical2**](https://msdn.microsoft.com/library/windows/hardware/ff561441)。

[ **FillPhysical** ](https://msdn.microsoft.com/library/windows/hardware/ff545394)方法可用于将一种模式的字节，多个时间复制到目标的物理内存。

目标的虚拟地址空间中的地址可以通过使用转换为目标系统上的物理地址[ **VirtualToPhysical** ](https://msdn.microsoft.com/library/windows/hardware/ff560335)方法。 用于转换的物理地址的虚拟地址系统的分页结构可通过使用[ **GetVirtualTranslationPhysicalOffsets**](https://msdn.microsoft.com/library/windows/hardware/ff549498)。

### <a name="span-ideventsspanspan-ideventsspanevents"></a><span id="events"></span><span id="EVENTS"></span>事件

当更改目标虚拟或物理内存时， [ **IDebugEventCallbacks::ChangeDebuggeeState** ](https://msdn.microsoft.com/library/windows/hardware/ff550678)调用回调方法。

 

 





