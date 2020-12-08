---
title: 链接的显示适配器
description: 链接显示适配器中 (LDA) 链接的每个物理适配器都可以独立支持 GpuMmu、IoMmu 或这两种寻址模式。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eebba0f11f8c17c953910da4c5e219fcd8da26b7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792293"
---
# <a name="linked-display-adapter"></a>链接的显示适配器


链接显示适配器中 (LDA) 链接的每个物理适配器都可以独立支持 *GpuMmu* 、 *IoMmu* 或这两种寻址模式。

## <a name="span-idiommu_supportspanspan-idiommu_supportspanspan-idiommu_supportspaniommu-support"></a><span id="IoMmu_support"></span><span id="iommu_support"></span><span id="IOMMU_SUPPORT"></span>IoMmu 支持


链接中的每个物理适配器都可以支持 *IoMmu* 模型和/或 *GpuMmu* 模型。

对于支持 *IoMmu* 模型的逻辑适配器，将调用 [*DxgkDdiCreateDevice*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_createdevice) 。

## <a name="span-idgpummu_supportspanspan-idgpummu_supportspanspan-idgpummu_supportspangpummu-support"></a><span id="GpuMmu_support"></span><span id="gpummu_support"></span><span id="GPUMMU_SUPPORT"></span>GpuMmu 支持


链接中的所有物理适配器共享相同的进程虚拟地址空间，但每个图形处理单元 (GPU) 具有其自己的页面表。 通常，每个 GPU 上页面表的内容有所不同。

![链接显示适配器内存地址段](images/linked-display-adapter.1.png)

每个物理适配器都允许具有其自己的 *GpuMmu* 功能 (页面表段、页面表更新节点、虚拟地址布局、基础页面表格式、大小等 ) 。 唯一的限制是所有物理适配器必须具有相同的虚拟地址大小。 对于所有适配器， **VirtualAddressBitCount** 必须相同。 驱动程序应将地址空间大小固定到物理 Gpu 的最小值。

现在，Microsoft DirectX 图形内核将在链接中查询每个物理适配器的 *GpuMmu* cap。 还将为每个物理适配器调用 [*DxgkDdiQueryAdapterInfo*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_queryadapterinfo) (**DXGKQAITYPE \_ PAGETABLELEVELDESC**) 。

**InputDataSize** 和 **pInputData** for [*DxgkDdiQueryAdapterInfo*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_queryadapterinfo) (**DXGKQAITYPE \_ GPUMMUCAPS**) 将指向 **DXGK \_ GPUMMUCAPSIN**。

**InputDataSize** 和 **pInputData** for [*DxgkDdiQueryAdapterInfo*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_queryadapterinfo) (**DXGKQAITYPE \_ PAGETABLELEVELDESC**) 将指向 **DXGK \_ PAGETABLELEVELDESCIN**。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[*DxgkDdiCreateDevice*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_createdevice)

 

