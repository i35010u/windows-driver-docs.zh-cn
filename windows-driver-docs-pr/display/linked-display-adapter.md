---
title: 链接的显示适配器
description: 链接的显示适配器 (LDA) 链接中每个物理适配器可以独立地支持 GpuMmu 或 IoMmu 或这两种寻址模式。
ms.assetid: 28B13BD7-6CC7-47C7-9FA3-BC55C73441DF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 983e94a1b280423261980c4518c7a2b09519b5e8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354267"
---
# <a name="linked-display-adapter"></a>链接的显示适配器


链接的显示适配器 (LDA) 链接中每个物理适配器可以支持*GpuMmu*或*IoMmu*或两个单独寻址模式。

## <a name="span-idiommusupportspanspan-idiommusupportspanspan-idiommusupportspaniommu-support"></a><span id="IoMmu_support"></span><span id="iommu_support"></span><span id="IOMMU_SUPPORT"></span>IoMmu 支持


链接中的每个物理适配器可以支持*IoMmu*模型和/或*GpuMmu*模型。

[*DxgkDdiCreateDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff559615)将为逻辑适配器，支持调用*IoMmu*模型。

## <a name="span-idgpummusupportspanspan-idgpummusupportspanspan-idgpummusupportspangpummu-support"></a><span id="GpuMmu_support"></span><span id="gpummu_support"></span><span id="GPUMMU_SUPPORT"></span>GpuMmu 支持


链接中的所有物理适配器都共享相同的进程虚拟地址空间，但每个图形处理单元 (GPU) 具有其自己的页表。 通常情况下，页表的内容是在每个 GPU 上不同。

![链接的显示适配器内存地址段](images/linked-display-adapter.1.png)

每个物理适配器允许拥有其自己*GpuMmu* （页表段、 页表更新节点、 虚拟地址布局、 基础页面表格格式、 大小等） 的功能。 唯一的限制是所有的物理适配器必须具有相同的虚拟地址大小。 **GpuMmuCaps.VirtualAddressBitCount**必须是所有适配器的相同。 该驱动程序应固定到的最小的地址空间大小的物理 Gpu。

现在将查询 Microsoft DirectX 图形内核*GpuMmu*上限为每个物理适配器的链接。 [*DxgkDdiQueryAdapterInfo* ](https://msdn.microsoft.com/library/windows/hardware/ff559746) (**DXGKQAITYPE\_PAGETABLELEVELDESC**) 还将为每个物理适配器调用。

**InputDataSize**并**pInputData**有关[ *DxgkDdiQueryAdapterInfo*](https://msdn.microsoft.com/library/windows/hardware/ff559746)(**DXGKQAITYPE\_GPUMMUCAPS**) 将指向**DXGK\_GPUMMUCAPSIN**。

**InputDataSize**并**pInputData**有关[ *DxgkDdiQueryAdapterInfo*](https://msdn.microsoft.com/library/windows/hardware/ff559746)(**DXGKQAITYPE\_PAGETABLELEVELDESC**)将指向**DXGK\_PAGETABLELEVELDESCIN**。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[*DxgkDdiCreateDevice*](https://msdn.microsoft.com/library/windows/hardware/ff559615)

 

 






