---
title: 分配系统空间内存
description: 分配系统空间内存
ms.assetid: eee425b3-6ddd-4e9d-b51d-1f2c9ea106a5
keywords:
- 内存管理 WDK 内核，系统分配的空间
- 系统分配的空间 WDK 内核
- 分配系统空间内存
- 分配 i/o 缓冲区内存
- I/o 缓冲内存分配 WDK 内核
- 缓冲区内存分配 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1f00fcdad9405abf62c25c522b25a6586be03d1f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837233"
---
# <a name="allocating-system-space-memory"></a>分配系统空间内存





驱动程序可以在其[设备扩展](device-extensions.md)中使用系统分配的空间，作为特定于设备的信息的全局存储区。 驱动程序只能使用内核堆栈向其内部例程传递少量数据。 某些驱动程序必须分配更多的系统空间内存，通常用于 i/o 缓冲区。

若要分配 i/o 缓冲空间，要使用的最佳内存分配例程为[**MmAllocateNonCachedMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-mmallocatenoncachedmemory)、 [**MmAllocateContiguousMemorySpecifyCache**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmallocatecontiguousmemoryspecifycache)、 [**AllocateCommonBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pallocate_common_buffer) （如果驱动程序的设备使用的是 bus 主机 dma 或系统 dma控制器的自动初始化模式）或[**ExAllocatePoolWithTag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)。

在系统运行时，非分页池通常会成为碎片，因此驱动程序的[**DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)例程应调用这些例程来设置驱动程序所需的任何长期 i/o 缓冲区。 其中的每个例程（ [**ExAllocatePoolWithTag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)除外）都分配与处理器特定边界（由处理器的数据缓存行大小确定）对齐的内存，以提供最佳性能。

驱动程序应尽可能经济地分配 i/o 缓冲区，因为非分页池内存是有限的系统资源。 通常，驱动程序应避免重复调用这些支持例程来请求小于页\_大小的分配，因为每个小于页\_大小的分配还附带了一个池标头，该标头用于内部管理分区.

### <a name="tips-for-allocating-driver-buffer-space-economically"></a>经济实惠地分配驱动程序缓冲区空间的提示

若要经济实惠地分配 i/o 缓冲内存，请注意以下事项：

-   每次调用[**MmAllocateNonCachedMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-mmallocatenoncachedmemory)或[**MmAllocateContiguousMemorySpecifyCache**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmallocatecontiguousmemoryspecifycache)时，均始终返回系统页面大小的完整多个页面大小，即未分页的系统空间内存，无论请求的分配的大小如何。 因此，小于一个页面的请求将向上舍入到整页，页面上的所有剩余字节数将会浪费;调用函数的驱动程序无法访问它们，并且其他内核模式代码无法使用这些驱动程序。

-   对[**AllocateCommonBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pallocate_common_buffer)的每次调用至少使用一个适配器对象映射寄存器，其中至少映射一个字节，最多可映射一页。 有关映射寄存器和使用常见缓冲区的详细信息，请参阅[适配器对象和 DMA](adapter-objects-and-dma.md)。

### <a name="allocating-memory-with-exallocatepoolwithtag"></a>用 ExAllocatePoolWithTag 分配内存

驱动程序还可以调用[**ExAllocatePoolWithTag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)，并指定以下系统定义的[**池之一\_键入**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ne-wdm-_pool_type) *PoolType*参数的值：

-   对于未存储在设备扩展或控制器扩展中的任何对象或资源，如果该驱动程序在以 IRQL &gt; APC\_级别运行时，则*PoolType* = **非分页池**。

    对于此*PoolType*值，当指定的*NumberOfBytes*小于或等于页\_大小时， [**ExAllocatePoolWithTag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)将分配所请求的内存量。 否则，会浪费上次分配的页上的所有剩余字节数：调用方无法访问这些字节，其他内核模式代码无法使用这些字节。

    例如，在 x86 上，5 kb 的分配请求将返回两个 4 KB 的页面。 第二页的最后 3 KB 对于调用方或其他调用方不可用。 为了避免浪费非分页池，驱动程序应该有效地分配多个页面。 例如，在这种情况下，驱动程序可能会进行两次分配，一个用于页\_大小，另一个用于 1 KB，分配总共 5 KB。

    **请注意**  从 Windows Vista 开始，系统会自动添加额外的内存，因此不需要两个分配。

     

-   *PoolType* = **PagedPool** ，适用于始终以 IRQL &lt;= APC\_级别访问且不在文件系统写入路径中的内存。

如果**ExAllocatePoolWithTag**不能分配请求的字节数，则返回**NULL**指针。 驱动程序应始终检查返回的指针。 如果其值为**NULL**， **DriverEntry**例程（或返回 NTSTATUS 值的任何其他驱动程序例程）应返回状态\_\_资源不足，或者尽可能处理错误条件。

 

 




