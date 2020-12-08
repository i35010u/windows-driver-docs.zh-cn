---
title: 实际堆基址的通知
description: 实际堆基址的通知
keywords:
- 堆 WDK DirectDraw
- 显示内存 WDK DirectDraw，堆
- 非本地显示内存 WDK DirectDraw，堆
- AGP WDK DirectDraw，堆
- 绘制 AGP 支持 WDK DirectDraw，堆
- DirectDraw AGP 支持 WDK Windows 2000 显示，堆
- 内存 WDK DirectDraw AGP、堆
- 通知 WDK DirectDraw 堆地址
- 线性堆 WDK DirectDraw
- 物理堆 DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cdfd91ed03b931baade96ac34814539f770009db
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840375"
---
# <a name="notification-of-actual-heap-base-addresses"></a>实际堆基址的通知


## <span id="ddk_notification_of_actual_heap_base_addresses_gg"></span><span id="DDK_NOTIFICATION_OF_ACTUAL_HEAP_BASE_ADDRESSES_GG"></span>


在 DirectDraw 初始化时，驱动程序可能需要了解堆基的线性和物理地址 (例如，模式更改期间) ，而不是等待 surface 创建请求并查看全局 DirectDraw 表面对象中的堆。 为支持此功能，DirectDraw 使用全局唯一标识符 (GUID) 标识驱动程序返回的信息，从而调用驱动程序提供的 [**DdGetDriverInfo**](/windows/win32/api/ddrawint/nc-ddrawint-pdd_getdriverinfo) 回调函数。 如果驱动程序识别 GUID 并且有要返回的信息，则它会将此信息复制到提供的数据结构中，并将其传回 DirectDraw。

驱动程序使用两个 Guid 来收集和提供有关直接绘制堆的详细信息：

-   GUID \_ GetHeapAlignment

-   GUID \_ UpdateNonLocalHeap

GUID \_ GetHeapAlignment 向驱动程序发出信号，以便收集有关传递给它的任何 DirectDraw 堆的堆对齐信息。 使用 [**DD \_ GETHEAPALIGNMENTDATA**](/windows/win32/api/dmemmgr/ns-dmemmgr-dd_getheapalignmentdata) 结构将堆信息传递给驱动程序。 GUID \_ GetHeapAlignment 定义为：

```cpp
DEFINE_GUID( GUID_GetHeapAlignment,
    0x42e02f16, 0x7b41, 0x11d2, 0x8b, 0xff, 0x0, 0xa0, 0xc9, 0x83, 0xea, 0xf6);
```

GUID \_ UpdateNonLocalHeap 使用 DirectDraw 提供的非本地堆结构发出信号，指示驱动程序使用堆信息更新其内部状态。 此信息包含在 [**DD \_ UPDATENONLOCALHEAPDATA**](/windows/win32/api/ddrawint/ns-ddrawint-dd_updatenonlocalheapdata) 结构中。 GUID \_ UpdateNonLocalHeap 定义为：

```cpp
DEFINE_GUID( GUID_UpdateNonLocalHeap,
           0x42e02f17, 0x7b41, 0x11d2, 0x8b, 0xff, 0x0, 0xa0, 0xc9, 0x83, 0xea, 0xf6);
```

如果驱动程序必须自行为 AGP 表面分配内存，但已向 DirectDraw 公开了堆，则 [**HeapVidMemAllocAligned**](/windows/win32/api/dmemmgr/nf-dmemmgr-heapvidmemallocaligned) 将作为 **Eng** 函数公开以用于此目的。 **HeapVidMemAllocAligned** 仅处理堆地址，使其返回偏移量。 驱动程序必须执行所需的任何内存映射工作，才能将从 **HeapVidMemAllocAligned** 返回的信息转换为虚拟地址。

 

