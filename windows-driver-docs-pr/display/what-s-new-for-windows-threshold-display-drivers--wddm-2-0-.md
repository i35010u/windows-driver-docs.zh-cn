---
title: What's new for Windows 10 显示器驱动程序 (WDDM 2.x)
description: 描述了显示器驱动程序的 Windows 10 中新功能
ms.assetid: 619175D4-98DA-4B17-8F6F-71B13A31374D
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18, 19H1
ms.openlocfilehash: 0fe540b7ecd20887032f968ac2efa4f234f30f59
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59903075"
---
# <a name="whats-new-for-windows-10-display-drivers-wddm-20-and-later"></a>What's new for Windows 10 显示器驱动程序 (WDDM 2.0 及更高版本)

## <a name="wddm-26"></a>WDDM 2.6

### <a name="super-wet-ink"></a>Super 湿的墨迹

*超湿的墨迹*是一项功能，围绕*front 缓冲区呈现*。 IHV 驱动程序可以支持的格式或硬件不支持的模式下的"可显示"纹理的创建。 通过将分配给应用程序请求的纹理，以及具有格式/布局可显示"影子"纹理，然后将复制在存在时两者之间，它们可以执行此操作。 此"影子"不一定是纹理以正常方式我们认为它，但可能只是压缩数据。 此外，它可能不需要存在，但可能是一种优化方式相反。

在运行时将会发生变化，若要了解这些方面的可显示的图面：

* 阴影必须存在针对特定 VidPnSource/平面上的显示。

* 是否为阴影存在更优。

* 当应用程序图面中的内容传输到卷影图面。

    * 在运行时将是显式的有关此操作，而不是它已超出存在隐式的。

* 如何请求设置一种模式或动态翻转之间的原始和阴影的图面。

Scanout 很快 VBlank，扫描垂直方向从上到下图中，可能会开始和完成下一步 VBlank 之前短暂。 这并不总是的情况下，具体取决于像素时钟的时间和纹理; 中的数据的布局尤其是如果没有可用的实际压缩。 

添加了新 DDIs 分隔并了解转换发生之前 scanout，以便为 （如果可能） 启用前端缓冲区呈现。 请参阅[D3DWDDM2_6DDI_SCANOUT_FLAGS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ne-d3d10umddi-d3dwddm2_6ddi_scanout_flags)并[PFND3DWDDM2_6DDI_PREPARE_SCANOUT_TRANSFORMATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3dwddm2_6ddi_prepare_scanout_transformation)。

### <a name="variable-rate-shading"></a>明暗度变量速率

明暗度变量速率或粗略像素明暗度是一种机制来启用的呈现性能/电源以不同速率呈现的映像间分配。

在先前的模型，以便使用 MSAA （多重采样抗锯齿） 以减少几何别名：

* 可减少几何锯齿量需要知道预先分配目标时。
* 分配目标后，不能更改可减少几何锯齿量。

WDDM 2.6 中的新模型 MSAA 扩展到相反*粗略像素*方向，通过添加了新的概念*粗略的明暗度*。 这是其中明暗度可以执行的频率比一个像素更粗。 可以作为单个单元着色的像素为单位的组和结果然后广播到组中的所有示例。

粗略的明暗度 API 允许应用程序指定的归属于一个着色的像素数。 粗像素大小可各不相同后该呈现器目标分配。 因此，不同的屏幕或不同的绘图传递部分可以有不同的课程明暗度速率。

可具有两个用户可查询顶端的多层实现。 层 1 和 2，粗略的明暗度是适用于单采样和 MSAA 资源。 MSAA 资源的明暗度可以执行每个粗糙的像素或每个样本像往常一样。 但是，在层 1 和 2，MSAA 资源的粗采样不能使用为每像素和每个样本之间的频率的底纹。

第 1 层：

* 只能基于每个-绘图-; 指定明暗度速率比这更精细的执行任何操作

* 明暗度速率统一适用于独立于其位于该呈现器目标的绘制内容  

第 2 层：

* 可以在每个-绘图的模式中，如第 1 层中所示指定明暗度的速率。 它还可以通过组合的每个绘图的基础，以及指定：

    * 每个人深受启发的顶点，从语义和
    * Screenspace 图像

* 从三个来源的明暗度费率组合使用一系列的合并器
* 屏幕空间图像平铺大小是 16 x 16 或更小。 保证的明暗度速率请求的应用程序是完全 （对于临时和其他重新构造筛选器的精度） 交付 

* 支持 SV_ShadingRate PS 输入。 如果使用一个视区，并且 SV_ViewportIndex 不会写入到的每个启发顶点速率，以每个基元速率，此处也称为才有效。

* 每个启发顶点速率，也称为每个基元费率，可用于多个视区，如果 SupportsPerVertexShadingRateWithMultipleViewports cap 标记，则返回 true。 此外，在这种情况下，它可用时 SV_ViewportIndex 写入。

请参阅[PFND3D12DDI_RS_SET_SHADING_RATE_0062](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_rs_set_shading_rate_0062)并[D3D12DDI_SHADING_RATE_0062](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/ne-d3d12umddi-d3d12ddi_shading_rate_0062)。

### <a name="collect-diagnostic-info"></a>收集诊断信息

*收集诊断信息*，操作系统就可以从包含这两个呈现和显示功能的图形适配器驱动程序中收集专用数据。 这一新功能是在 WDDM 2.6 中的要求。 

新 DDI 应允许 OS 在收集信息随时加载驱动程序。 操作系统将当前使用 DxgkDdiCollectDebugInfo 函数为 TDR （超时检测和恢复） 由查询驱动程序的专用数据微型端口实现的相关案例。 新 DDI 将用于收集数据的原因多种多样。 诊断需要提供所请求的信息类型时，操作系统将调用此 DDI。 该驱动程序应该收集重要调查该问题并将其提交到 OS 的所有私有信息。 将最终弃用，替换为 DxgkDdiCollectDiagnosticInfo DxgkDdiCollectDebugInfo。

请参阅[DXGKDDI_COLLECTDIAGNOSTICINFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_collectdiagnosticinfo)。

### <a name="background-processing"></a>后台处理

后台处理允许用户模式驱动程序来表达所需的行为，并在运行时线程处理来控制/监视器它。 用户模式驱动程序将启动后台线程和分配为低的线程优先级作为可能的并且依赖于 NT 计划程序，以确保这些线程不会中断通常带成功的关键路径线程。

Api 允许应用将调整后台处理量是适用于其工作负荷，以及何时执行该工作。

请参阅[PFND3D12DDI_QUEUEPROCESSINGWORK_CB_0062](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_queueprocessingwork_cb_0062)。

### <a name="driver-hot-update"></a>驱动程序热更新

操作系统组件需要更新时，驱动程序热更新可减少服务器停机时间最大程度地。

驱动程序热修补程序用于将安全修补程序应用到内核模式驱动程序。 在这种情况下，驱动程序要求以保存适配器内存、 停止适配器时、 驱动程序已卸载、 加载新的驱动程序和重新启动该适配器。

请参阅[DXGKDDI_SAVEMEMORYFORHOTUPDATE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkcb_savememoryforhotupdate)并[DXGKDDI_RESTOREMEMORYFORHOTUPDATE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_restorememoryforhotupdate)。

## <a name="wddm-25"></a>WDDM 2.5

### <a name="content-changes"></a>内容更改

| 主题 | date | 描述 |
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
