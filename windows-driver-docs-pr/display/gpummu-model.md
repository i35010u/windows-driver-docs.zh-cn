---
title: GpuMmu 模型
description: 在 GpuMmu 模型中，图形处理单元 (GPU) 具有其自己的内存管理单元 (MMU) 这会转换到物理地址的每个进程的 GPU 虚拟地址。
ms.assetid: FFDFD647-2F00-4AC3-A41A-4224562A51ED
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 56b48612b1d3b9f2bd48934ec681a3ca21843b6c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379959"
---
# <a name="gpummu-model"></a>GpuMmu 模型


在中*GpuMmu*模型中，图形处理单元 (GPU) 具有其自己的内存管理单元 (MMU) 这会转换到物理地址的每个进程的 GPU 虚拟地址。

每个进程具有单独 CPU 和 GPU 虚拟地址空间，使用不同的页表。 视频内存管理器管理的所有进程的 GPU 虚拟地址空间，并负责分配、 扩大、 更新、 确保驻留和释放页表。 通过 GPU MMU，所使用的页表的硬件格式是未知的视频内存管理器，并通过设备驱动程序接口 (DDIs) 抽象化。 抽象支持多级的级别转换，包括固定的大小的页表和可调整大小的根页表。

视频内存管理器负责管理 GPU 虚拟地址空间和其基础的页表，尽管视频内存管理器不分配的自动分配 GPU 虚拟地址。 这一责任落到用户模式驱动程序。

视频内存管理器提供服务添加到用户模式驱动程序的两个的集。 首先，用户模式驱动程序可能会分配通过现有的视频内存[*分配*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_allocatecb)回调和释放该内存通过现有[ *Deallocate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_deallocatecb)回调。 像现在一样，这返回用户模式驱动程序的句柄的视频内存管理器分配，可以在运营的 GPU 引擎。 此类分配表示只有分配的物理部分，并且可能由运行在物理上，通过分配列表引用一个引擎引用。

在虚拟模式下运行时引擎，GPU 的虚拟地址需要将明确分配给分配之前可能几乎对其进行访问。 为此目的的视频内存管理器提供了用户模式驱动程序服务到预留或可用 GPU 虚拟地址和映射特定分配范围到进程的 GPU 虚拟地址空间。 这些服务是非常灵活，允许对进程 GPU 虚拟地址空间的用户模式驱动程序细粒度控制。 用户模式驱动程序可能决定将非常具体的 GPU 虚拟地址分配给分配，或让视频内存管理器会自动选择可用的一个，可能指定一些最小值和最大的 GPU 虚拟地址限制。 单个分配可能有与之关联的多个 GPU 的虚拟地址映射和服务提供给用户模式驱动程序来实现*磁贴资源协定*。

同样，在链接的显示适配器配置中，用户模式驱动程序显式可能将 GPU 虚拟地址映射到特定的分配实例，并选择每个映射是否映射应为其本身或特定对等 GPU。 在此模型中，分配给分配的 CPU 和 GPU 虚拟地址是独立的。 用户模式驱动程序可能会决定将它们保留相同在这两个地址空间或使它们独立。

GPU 虚拟地址会以逻辑方式在固定的 4 KB 页粒度通过 DDI 界面进行管理。 GPU 虚拟地址可能会引用分配，后者是驻留在内存段或系统内存。 虽然在驱动程序的选择在 4 KB 或 64 kb 为单位进行管理内存段，在 4 KB 物理粒度管理系统内存。 所有视频内存管理器分配是对齐和大小调整，以将所选驱动程序的页大小的倍数。

访问无效的 GPU 虚拟地址导致访问冲突并终止的上下文和/或导致访问错误的设备。 若要从这类错误中恢复，视频内存管理器会启动一个引擎重置其获取提升为适配器宽超时检测恢复 (TDR)，如果不成功。

*GpuMmu*模型如下图所示：

![gpummu 模型](images/gpummu-model.1.png)

 

 





