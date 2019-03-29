---
title: 实际堆基址的通知
description: 实际堆基址的通知
ms.assetid: b2fe29c7-7c97-41c2-a6be-2c0ef25c5b58
keywords:
- 堆 WDK DirectDraw
- 显示内存 WDK DirectDraw 堆
- 非本地显示内存 WDK DirectDraw 堆
- AGP WDK DirectDraw 堆
- 绘制 AGP 支持 WDK DirectDraw，堆
- DirectDraw AGP 支持 WDK Windows 2000 显示堆
- WDK DirectDraw AGP，堆内存
- 通知 WDK DirectDraw 堆地址
- 线性堆 WDK DirectDraw
- 物理堆 WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff0afa25a9bbf81866bebb263b8066eb1bfa19d5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567379"
---
# <a name="notification-of-actual-heap-base-addresses"></a>实际堆基址的通知


## <span id="ddk_notification_of_actual_heap_base_addresses_gg"></span><span id="DDK_NOTIFICATION_OF_ACTUAL_HEAP_BASE_ADDRESSES_GG"></span>


驱动程序可能需要在 DirectDraw 初始化时 （例如，在模式更改） 知道在堆的基的线性和物理地址而不是等待的图面上创建请求，并查看全局 DirectDraw 图面上对象中的堆。 若要支持此功能，DirectDraw 调用的驱动程序提供[ **DdGetDriverInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff549404)回调函数标识要返回的驱动程序的信息的全局唯一标识符 (GUID)。 如果该驱动程序可以识别的 GUID，并且具有要返回的信息，它将此信息复制到提供的数据结构，并将其传递回 DirectDraw。

该驱动程序使用以下两个 Guid 来收集和提供有关直接绘制堆的详细信息：

-   GUID\_GetHeapAlignment

-   GUID\_UpdateNonLocalHeap

GUID\_GetHeapAlignment 信号向驱动程序以收集有关任何 DirectDraw 堆对齐信息堆传递给它。 堆信息传递给驱动程序使用[ **DD\_GETHEAPALIGNMENTDATA** ](https://msdn.microsoft.com/library/windows/hardware/ff551572)结构。 GUID\_GetHeapAlignment 定义为：

```cpp
DEFINE_GUID( GUID_GetHeapAlignment,
    0x42e02f16, 0x7b41, 0x11d2, 0x8b, 0xff, 0x0, 0xa0, 0xc9, 0x83, 0xea, 0xf6);
```

GUID\_UpdateNonLocalHeap 发出信号要更新其内部状态与堆信息一起使用 DirectDraw 由提供的非本地堆结构的驱动程序。 此信息包含在[ **DD\_UPDATENONLOCALHEAPDATA** ](https://msdn.microsoft.com/library/windows/hardware/ff551748)结构。 GUID\_UpdateNonLocalHeap 定义为：

```cpp
DEFINE_GUID( GUID_UpdateNonLocalHeap,
           0x42e02f17, 0x7b41, 0x11d2, 0x8b, 0xff, 0x0, 0xa0, 0xc9, 0x83, 0xea, 0xf6);
```

如果该驱动程序必须 AGP 显示其本身而言，但然后公开到 DirectDraw，堆分配内存[ **HeapVidMemAllocAligned** ](https://msdn.microsoft.com/library/windows/hardware/ff567267)作为公开**Eng**函数此目的。 **HeapVidMemAllocAligned**只处理与堆地址，使其返回某一偏移量。 该驱动程序必须执行任何内存映射的工作需要的操作将从返回的信息**HeapVidMemAllocAligned**转换为虚拟地址。

 

 





