---
title: 分配系统空间内存
description: 分配系统空间内存
ms.assetid: eee425b3-6ddd-4e9d-b51d-1f2c9ea106a5
keywords:
- 内存管理 WDK 内核，系统分配的空间
- 系统分配的空间 WDK 内核
- 分配系统空间内存
- 分配 I/O 缓冲区内存
- I/O 缓冲区内存分配 WDK 内核
- 缓冲区内存分配 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f9dc9dfcf7f903ac0dc34adfdae9b6bdc3888f0b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348564"
---
# <a name="allocating-system-space-memory"></a>分配系统空间内存





驱动程序可以使用系统分配的空间中其[设备扩展](device-extensions.md)作为全局存储区域的特定于设备的信息。 驱动程序可以使用仅内核堆栈将传递给其内部的例程的少量数据。 某些驱动程序必须分配更多、 更大的系统空间内存量，通常用于 I/O 缓冲区。

若要分配 I/O 的缓冲区空间，最佳的内存分配例程以使用所[ **MmAllocateNonCachedMemory**](https://msdn.microsoft.com/library/windows/hardware/ff554479)， [ **MmAllocateContiguousMemorySpecifyCache**](https://msdn.microsoft.com/library/windows/hardware/ff554464)， [ **AllocateCommonBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff540575) （如果驱动程序的设备使用总线 master DMA 或系统 DMA 控制器的自动初始化模式），或[ **ExAllocatePoolWithTag**](https://msdn.microsoft.com/library/windows/hardware/ff544520)。

非分页缓冲的池通常会是非常零散系统运行时，这样的驱动程序[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)例程应调用这些例程来设置任何长期的 I/O 缓冲区驱动程序需要。 每个例程，除[ **ExAllocatePoolWithTag**](https://msdn.microsoft.com/library/windows/hardware/ff544520)，分配 （由处理器的数据缓存行大小） 的特定于处理器的边界对齐以提供最佳的内存性能。

驱动程序应尽可能经济分配 I/O 缓冲区，因为非分页缓冲的池内存是有限的系统资源。 通常情况下，驱动程序应避免调用这些支持例程重复以请求分配的页少于\_调整大小，因为页少于每个分配\_大小还附带了对在内部使用的池标头管理分配。

### <a name="tips-for-allocating-driver-buffer-space-economically"></a>经济实惠的方式分配驱动程序缓冲区空间的提示

若要经济实惠的方式分配 I/O 的缓冲区内存，应注意以下：

-   每次调用[ **MmAllocateNonCachedMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff554479)或[ **MmAllocateContiguousMemorySpecifyCache** ](https://msdn.microsoft.com/library/windows/hardware/ff554464)始终返回完整的倍数系统的页面大小，非分页的系统空间内存，任何请求分配的大小。 因此，小于页面会向上舍入到的请求会浪费掉整页和页上的任何其余部分字节;将通过调用的函数和其他内核模式代码无法使用的驱动程序无法访问它们。

-   每次调用[ **AllocateCommonBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff540575)使用至少一个适配器对象映射寄存器，它映射至少 1 个字节，最多一页。 有关映射的详细信息将注册并使用常见的缓冲区，请参阅[适配器对象和 DMA](adapter-objects-and-dma.md)。

### <a name="allocating-memory-with-exallocatepoolwithtag"></a>分配内存以及 ExAllocatePoolWithTag

驱动程序还可以调用[ **ExAllocatePoolWithTag**](https://msdn.microsoft.com/library/windows/hardware/ff544520)，指定下列系统定义任一[**池\_类型**](https://msdn.microsoft.com/library/windows/hardware/ff559707)值为*PoolType*参数：

-   *PoolType* = **非分页池**的任何对象或资源未存储在设备扩展插件或驱动程序可能在 IRQL 运行时访问的控制器扩展&gt;APC\_级别。

    为此*PoolType*值， [ **ExAllocatePoolWithTag** ](https://msdn.microsoft.com/library/windows/hardware/ff544520)分配的内存，如果请求量指定*字节数*小于或等于页面\_大小。 否则，浪费在上一次分配页上的任何其余部分字节： 调用方都无法访问和其他内核模式代码不可用。

    例如，x86，5 千字节 (KB) 的分配请求返回两个 4 KB 页为单位。 最后一个 3KB 的第二页是对调用方或另一个调用方不可用。 若要避免浪费非分页缓冲的池，该驱动程序应有效地分配多个页面。 在这种情况下，例如，驱动程序可以进行两个分配，一个用于页\_大小，另一个用于 1 KB 分配总共 5 KB。

    **请注意**  从 Windows Vista 开始，系统会自动添加更多的内存以便不是必需的两个分配。

     

-   *PoolType* = **PagedPool**始终在 IRQL 访问的内存&lt;= APC\_级别并不在文件系统的写路径。

**ExAllocatePoolWithTag**将返回**NULL**如果它不能分配请求的字节数的指针。 驱动程序应始终检查返回的指针。 如果其值为**NULL**，则**DriverEntry**例程 （或任何其他驱动程序例程，以返回 NTSTATUS 值） 应返回状态\_不足\_资源或句柄如有可能错误条件。

 

 




