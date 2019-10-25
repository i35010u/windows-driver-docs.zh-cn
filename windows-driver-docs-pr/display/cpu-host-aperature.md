---
title: CPU 主机孔径
description: 对于不支持可调整大小的栏的32位 OS 离散图形处理单元（Gpu），或当调整框架缓冲区栏的大小时，Windows 显示驱动程序模型（WDDM） v2 会提供一种替代机制，通过该机制可以有效地访问离散 GPU VRAM. 对于支持可编程条地址空间的 Gpu，WDDM v2 中引入了一个新的 CPU 主机口径功能，以抽象该功能。
ms.assetid: 0E4D01E4-93AF-4205-A360-0CA3470716D2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9e1d599eba770d452e481b1584ece7bb2c696752
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839781"
---
# <a name="cpu-host-aperture"></a>CPU 主机孔径


对于不支持可调整大小的栏的32位 OS 离散图形处理单元（Gpu），或当调整框架缓冲区栏的大小时，Windows 显示驱动程序模型（WDDM） v2 会提供一种替代机制，通过该机制可以有效地访问离散 GPU VRAM. 对于支持可编程条地址空间的 Gpu，WDDM v2 中引入了一个新的 CPU 主机口径功能，以抽象该功能。

公开 CPU 主机口径时，内核模式驱动程序会为支持 CPU 主机口径的每个段填写新的[**DXGK\_CPUHOSTAPERTURE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_cpuhostaperture) cap 结构。 这会定义 CPU 主机口径的大小，这样，驱动程序便可出于内部目的保留某些部分。 页面大小与内存段的 GPU 页面相同。

然后，内核模式驱动程序公开两个新的设备驱动程序接口（DDIs）来管理条形地址空间，特别是[*DxgkDdiMapCpuHostAperture*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_mapcpuhostaperture)和[*DxgkDdiUnmapCpuHostAperture*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_unmapcpuhostaperture)。

CPU 主机口径后面的页表的内存是在驱动程序初始化过程中及早由驱动程序和设置管理的。 [*DxgkDdiMapCpuHostAperture*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_mapcpuhostaperture)和[*DxgkDdiUnmapCpuHostAperture*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_unmapcpuhostaperture)都应立即在段枚举后正常运行，并在视频内存管理器初始化过程中使用，以将 CPU 虚拟地址映射到页面适配器初始化期间系统分页过程的目录和页表。

当需要对内存段的 CPU 访问时，视频内存管理器会在 CPU 主机口径中保留页面，并通过它映射内存段页。 如下所示。

![cpu 主机口径段映射](images/cpu-host-aperture.1.png)

在链接的显示适配器配置中，类似于以下内容：

-   *默认值*或*LinkMirrored*分配始终映射到 GPU0。
-   *LinkInstanced*分配的虚拟地址范围为**AllocationSize**\***NumberOfGPUInLink**关联，并将分配的不同部分映射到不同的 GPU。

如下所示：为链接的显示适配器配置 ![cpu 主机口径段映射](images/cpu-host-aperture.2.png)

 

 





