---
title: What's new for Windows 10 显示器驱动程序 (WDDM 2.x)
description: 描述了显示器驱动程序的 Windows 10 中新功能
ms.assetid: 619175D4-98DA-4B17-8F6F-71B13A31374D
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: b4482bf4ba125771a38f8d66efe9c81ec394718d
ms.sourcegitcommit: 68bfa1f69229b7ac29d0e98f049734f5bc566a30
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/19/2019
ms.locfileid: "58187466"
---
# <a name="whats-new-for-windows-10-display-drivers-wddm-20-and-later"></a>What's new for Windows 10 显示器驱动程序 (WDDM 2.0 及更高版本)

## <a name="wddm-25"></a>WDDM 2.5

### <a name="content-changes"></a>内容更改

| 主题 | 日期 | 描述 |
| --- | --- | --- |
| [EDID HMDs 和专用的显示扩展插件 (VSDB)](specialized-monitors-edid-extension.md) | 12/03/2018 | 显示设备制造商的规范 |
| [DirectX 图形内核子系统 (Dxgkrnl.sys)](directx-graphics-kernel-subsystem.md) | 12/04/2018 | 通过 Microsoft DirectX 图形内核子系统 (Dxgkrnl.sys) 实现的 Windows 操作系统的内核模式接口。 |
| [WDDM 2.1 功能](wddm-2-1-features.md) | 01/10/2019|介绍了 WDDM 2.1 的新增和更新功能 |

### <a name="raytracing"></a>Raytracing

为了支持硬件加速 raytracing Direct3D API、 并行创建新 Direct3D DDI。 示例 DDI 包括： 

* [PFND3D12DDI_BUILD_RAYTRACING_ACCELERATION_STRUCTURE_0054](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_build_raytracing_acceleration_structure_0054) 
* [PFND3D12DDI_COPY_RAYTRACING_ACCELERATION_STRUCTURE_0054](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_copy_raytracing_acceleration_structure_0054)
* [PFND3D12DDI_EMIT_RAYTRACING_ACCELERATION_STRUCTURE_POSTBUILD_INFO_0054](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_emit_raytracing_acceleration_structure_postbuild_info_0054)
* [PFND3D12DDI_GET_RAYTRACING_ACCELERATION_STRUCTURE_PREBUILD_INFO_0054](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_get_raytracing_acceleration_structure_prebuild_info_0054)

有关 raytracing 的详细信息，请参阅：

* [宣布推出 Microsoft DirectX Raytracing](https://blogs.msdn.microsoft.com/directx/2018/03/19/announcing-microsoft-directx-raytracing/)
* [DirectX Raytracing 和 Windows 10 2018 年 10 月更新](https://blogs.msdn.microsoft.com/directx/2018/10/02/directx-raytracing-and-the-windows-10-october-2018-update/)
* [DirectX 论坛](https://forums.directxtech.com/index.php?topic=5985.0)

### <a name="display-synchronization"></a>显示同步

显示同步功能时显示公开到操作系统，因此之前启用显示器驱动程序将检查操作系统。 对于 TypeIntegratedDisplay 子设备，这报告通过调用[DxgkDdiQueryAdapterInfo](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_queryadapterinfo)与*类型* [DXGKQAITYPE_INTEGRATED_DISPLAY_DESCRIPTOR2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ne-d3dkmddi-_dxgk_queryadapterinfotype)在适配器初始化。 对于 TypeVideoOutput 子设备，开始 WDDM 2.5 支持功能报告的热插拔通过处理一部分[DxgkDdiUpdateMonitorLinkInfo](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_updatemonitorlinkinfo)以便功能可能会更改基于目标或连接的监视器。

OS 指定中的显示同步[DxgkDdiSetTimingsFromVidPn](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_settimingsfromvidpn)调用中的输入字段中每个路径[DXGK_SET_TIMING_PATH_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_set_timing_path_info#input)结构。

## <a name="wddm-21"></a>WDDM 2.1

WDDM 2.1 支持新方案，并提供几个方面的性能、 可靠性、 升级复原能力、 诊断改进和未来的系统的 Windows 图形子系统的改进功能的重大改进。
WDDM 2.0 驱动程序模型是对 D3D12 的先决条件。 WDDM 2.0 和 DirectX12 是仅适用于 Windows 10 及更高版本。

下面是列表的 WDDM 2.1 的新增功能和更新。

* 通过减少系统开销时间改进的图形性能所用的内存管理效率更高的稀缺图形内存的使用情况。 图形性能改进是：

    * 提供和回收资源-提供和回收改进，可减少内存占用量在后台模式下运行的应用程序。
    * 启用支持 2MB 页表条目编码-在 WDDM 2.1，大型页表项 (PTE) vram 能够中的编码。 此更改可以提高支持它的系统上的性能。
    * WDDM 2.1 还支持对 64 KB 内存页的虚拟内存分配使用 64KB 粒度的支持。 此更改尤其受益 Apu 和 Soc，通过减少开销来访问虚拟内存页面。

* 基于硬件的受保护的内容改进*提供批处理*([PlayReady 3.0](https://docs.microsoft.com/playready/))

* 若要提高驱动程序升级复原能力的图形驱动程序的驱动程序存储区安装。

* DXIL，新的着色器编译器语言

* D3D12 性能和优化的改进

* 改进了开发人员的诊断选项

有关详细信息，请参阅[WDDM 2.1 功能](wddm-2-1-features.md)。

## <a name="wddm-20"></a>WDDM 2.0

WDDM 2.0 包括内存管理更新。

### <a name="gpu-virtual-memory"></a>GPU 虚拟内存

-   所有的物理内存已抽象化为虚拟图形处理单元 (GPU) 内存管理器可以管理的段。
-   每个进程都获取自己 GPU 的虚拟地址空间。
-   已删除对 swizzling 范围的支持。

有关更多详细信息，请参阅[WDDM 2.0 中的 GPU 虚拟内存](gpu-virtual-memory-in-wddm-2-0.md)。

### <a name="driver-residency"></a>驱动程序驻留

-   视频内存管理器可确保在提交给驱动程序的命令缓冲区之前分配是驻留在内存中。 为了帮助实现此功能，新用户模式驱动程序设备驱动程序接口 (DDIs) 已添加 ([*MakeResident*](https://msdn.microsoft.com/library/windows/hardware/dn906357)， [ *TrimResidency* ](https://msdn.microsoft.com/library/windows/hardware/dn906364)， [*逐出*](https://msdn.microsoft.com/library/windows/hardware/dn906355))。
-   分配和修补程序的位置列表是被淘汰了，因为它不需要在新的模型。
-   用户模式驱动程序现在负责处理分配跟踪，并且添加了几个新 DDIs 以启用此功能。
-   驱动程序非常给定内存预算，预期内存压力下调整。 这样，通用 Windows 的驱动程序跨应用程序平台。
-   用于进程的同步和上下文监视添加了新 DDIs。

有关更多详细信息，请参阅[WDDM 2.0 中的驱动程序驻留](driver-residency-in-wddm-2-0.md)。