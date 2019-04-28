---
title: CPU 主机孔径
description: 对于 32 位操作系统离散图形处理的单元 (Gpu)，这不支持条可调整大小，或者当调整大小的帧缓冲区失败栏，Windows 显示驱动程序模型 (WDDM) v2 将提供替代机制，通过其离散的 GPU VRAM 可以有效地访问. 为 Gpu，支持可编程栏地址空间，WDDM v2 进行抽象该功能中引入了新的 CPU 主机 Aperture 功能。
ms.assetid: 0E4D01E4-93AF-4205-A360-0CA3470716D2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c745c74a503fef51b1e5557e60b1618a051c8fe2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346955"
---
# <a name="cpu-host-aperture"></a>CPU 主机孔径


对于 32 位操作系统离散图形处理的单元 (Gpu)，这不支持条可调整大小，或者当调整大小的帧缓冲区失败栏，Windows 显示驱动程序模型 (WDDM) v2 将提供替代机制，通过其离散的 GPU VRAM 可以有效地访问. 为 Gpu，支持可编程栏地址空间，WDDM v2 进行抽象该功能中引入了新的 CPU 主机 Aperture 功能。

当公开 CPU 主机 aperture，内核模式驱动程序将填出一个新[ **DXGK\_CPUHOSTAPERTURE** ](https://msdn.microsoft.com/library/windows/hardware/dn894624)指针顶端才支持 CPU 主机 aperture 的每个段的结构。 它定义的 CPU 主机 aperture 大小，这样一些栏保留供内部使用的驱动程序。 页大小为内存段的 GPU 页相同。

内核模式驱动程序然后公开两个新设备驱动程序接口 (DDIs)，管理栏地址空间，具体而言[ *DxgkDdiMapCpuHostAperture* ](https://msdn.microsoft.com/library/windows/hardware/dn906340)并[ *DxgkDdiUnmapCpuHostAperture*](https://msdn.microsoft.com/library/windows/hardware/dn906344)。

尽早在驱动程序初始化期间由驱动程序和设置管理 CPU 主机 aperture 后面的页表的内存。 这两[ *DxgkDdiMapCpuHostAperture* ](https://msdn.microsoft.com/library/windows/hardware/dn906340)并[ *DxgkDdiUnmapCpuHostAperture* ](https://msdn.microsoft.com/library/windows/hardware/dn906344)预期可立即后仍可运行细分枚举，并在视频内存管理器初始化过程中用于适配器初始化期间将 CPU 虚拟地址映射到的页面目录和系统分页进程的页表。

当 CPU 访问内存段是必需的时视频内存管理器保留的 CPU 主机 Aperture 中的页面，而映射通过它的内存段页。 这如下所示。

![cpu 主机 aperture 段映射](images/cpu-host-aperture.1.png)

在链接显示适配器配置操作类似以下情况除外。

-   *默认值*或*LinkMirrored*分配始终映射到 GPU0。
-   *LinkInstanced*分配具有的虚拟地址范围**AllocationSize**\***NumberOfGPUInLink**与各种部件与之相关联的分配映射到不同的 GPU。

这如下所示：![链接的显示适配器配置的 cpu 主机 aperture 段映射](images/cpu-host-aperture.2.png)

 

 





