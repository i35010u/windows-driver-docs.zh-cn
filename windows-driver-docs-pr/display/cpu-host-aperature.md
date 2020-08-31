---
title: CPU 主机孔径
description: 对于32位操作系统离散图形处理单元 (Gpu) ，这不支持可调整大小的栏，或调整框架缓冲区栏的大小时，Windows 显示驱动程序模型 (WDDM) v2 会提供一种可有效访问离散 GPU VRAM 的备用机制。 对于支持可编程条地址空间的 Gpu，WDDM v2 中引入了一个新的 CPU 主机口径功能，以抽象该功能。
ms.assetid: 0E4D01E4-93AF-4205-A360-0CA3470716D2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c050cac177479bf21948c3cd5286ba1f4c47a163
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89064358"
---
# <a name="cpu-host-aperture"></a>CPU 主机孔径


对于32位操作系统离散图形处理单元 (Gpu) ，这不支持可调整大小的栏，或调整框架缓冲区栏的大小时，Windows 显示驱动程序模型 (WDDM) v2 会提供一种可有效访问离散 GPU VRAM 的备用机制。 对于支持可编程条地址空间的 Gpu，WDDM v2 中引入了一个新的 CPU 主机口径功能，以抽象该功能。

公开 CPU 主机口径时，内核模式驱动程序会为支持 CPU 主机口径的每个段填充新的 [**DXGK \_ CPUHOSTAPERTURE**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_cpuhostaperture) cap 结构。 这会定义 CPU 主机口径的大小，这样，驱动程序便可出于内部目的保留某些部分。 页面大小与内存段的 GPU 页面相同。

然后，内核模式驱动程序公开两个新的设备驱动程序接口 (DDIs) 管理条形地址空间，特别是 [*DxgkDdiMapCpuHostAperture*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_mapcpuhostaperture) 和 [*DxgkDdiUnmapCpuHostAperture*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_unmapcpuhostaperture)。

CPU 主机口径后面的页表的内存是在驱动程序初始化过程中及早由驱动程序和设置管理的。 [*DxgkDdiMapCpuHostAperture*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_mapcpuhostaperture)和[*DxgkDdiUnmapCpuHostAperture*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_unmapcpuhostaperture)都应立即可在段枚举后正常运行，并在视频内存管理器初始化过程中使用，以便在适配器初始化期间将 CPU 虚拟地址映射到页面目录和系统分页过程的页表。

当需要对内存段的 CPU 访问时，视频内存管理器会在 CPU 主机口径中保留页面，并通过它映射内存段页。 下面对此做了演示。

![cpu 主机口径段映射](images/cpu-host-aperture.1.png)

在链接的显示适配器配置中，类似于以下内容：

-   *默认值* 或 *LinkMirrored* 分配始终映射到 GPU0。
-   *LinkInstanced*分配的虚拟地址范围为**AllocationSize** \* **NumberOfGPUInLink** ，并将分配的各个部分映射到不同的 GPU。

如下所示： ![ 链接的显示适配器配置的 cpu 主机口径段映射](images/cpu-host-aperture.2.png)

 

