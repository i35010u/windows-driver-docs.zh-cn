---
title: 先前的 WDDM 2.x 版本中添加的功能
description: 描述用于显示和图形驱动程序的以前的 Windows 10 版本中的功能
ms.assetid: 22793a7e-38fc-4cd8-aafd-09dfed48cb02
ms.date: 03/24/2020
ms.localizationpriority: medium
ms.custom: seodec18, 19H1
ms.openlocfilehash: f216dae793c91403b5b53685a59484fb76a09e31
ms.sourcegitcommit: d395d4b36f39d3557adda53735a4fdc8745a6408
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2020
ms.locfileid: "83666552"
---
# <a name="features-added-in-prior-wddm-2x-versions"></a>先前的 WDDM 2.x 版本中添加的功能

本页介绍了在以前版本的 Windows 10 中添加的显示和图形驱动程序功能。 若要查看最近的 WDDM 2.x 版本添加的新功能，请参阅[Windows 10 显示和图形驱动程序的新增](what-s-new-for-windows-10-display-and-graphics-drivers.md)功能。

## <a name="wddm-26"></a>WDDM 2。6

### <a name="super-wet-ink"></a>超级湿墨

*超湿墨迹*是一项围绕*前缓冲区呈现*的功能。 IHV 驱动程序可以支持创建硬件不支持的格式或模式的 "可显示" 纹理。 他们可以通过分配应用程序所请求的纹理来实现此目的，以及可以显示的格式/布局的 "阴影" 纹理，然后在两个当前时间之间进行复制。 这种 "阴影" 可能并不一定是我们想像的纹理，但可能只是压缩数据。 此外，它可能不是必需的，但可能是优化。

运行时将发展，以了解可显示的表面的这些方面：

* 在特定 VidPnSource/平面上显示时，是否必须存在阴影。

* 是否有更好的阴影效果。

* 何时将内容从应用程序表面传输到阴影图面。 对于此操作，运行时将是显式的，而与它在当前中是隐式的。

* 如何请求设置模式或在原始表面和阴影曲面之间动态翻转。

Scanout 可能会在 VBlank 之后不久开始，从图像的上到下垂直扫描，并在下一个 VBlank 之前完成。 这种情况并非总是出现，具体取决于像素时钟的时间和纹理中数据的布局;尤其是在实际有可用压缩时。

添加了新的 DDIs，以分离和理解 scanout 之前发生的转换，以便（如果可能）启用前缓冲区呈现。 请参阅 [D3DWDDM2_6DDI_SCANOUT_FLAGS](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3dwddm2_6ddi_scanout_flags) 和 [PFND3DWDDM2_6DDI_PREPARE_SCANOUT_TRANSFORMATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3dwddm2_6ddi_prepare_scanout_transformation)。

### <a name="variable-rate-shading"></a>可变速率底纹

可变速率底纹或粗像素底纹是一种机制，用于在呈现的图像之间以不同的速率分配渲染性能/功率。

在以前的模型中，为了使用 MSAA （多样本抗锯齿）来减少几何别名：

* 在分配目标时需要提前知道几何别名的减少量。
* 分配目标后，不能更改用于减少几何别名的量。

在 WDDM 2.6 中，新模型通过添加*粗底纹*的新概念将 MSAA 扩展到反向的*粗像素*方向。 在这种情况下，可以在比像素更粗糙的频率执行阴影。 一组像素可以作为单个单元着色，然后将结果广播到组中的所有样本。

粗阴影 API 允许应用指定属于阴影组的像素数。 在分配呈现器目标后，粗像素大小可能会改变。 这种情况下，屏幕的不同部分或不同的绘图会有不同的课程着色率。

多层实现提供了两个用户可查询的上限。 对于第1层和第2层，单采样资源和 MSAA 资源均可使用粗糙着色。 对于 MSAA 资源，可以像平常一样，按粗像素或按样本执行着色。 但是，在第1层和第2层上，对于 MSAA 资源，不能使用粗采样以每像素和每样本的频率进行阴影。

第1层：

* 只能在每个绘图上指定底纹速度;比此更精细

* 底纹速率统一应用于与渲染目标中的位置无关的绘图  

第2层：

* 可以按每个绘图指定底纹速度，如第1层中所示。 它还可以通过每个绘制基础和的组合指定：

  * 造成中的语义和
  * Screenspace 图像

* 三个源的底纹费率使用一组合并器组合在一起。
* 屏幕空间图像磁贴大小为16x16 或更小。 保证应用程序所请求的底纹速度是精确传递的（适用于临时和其他重建筛选器）

* 支持 SV_ShadingRate PS 输入。 每个造成的顶点速率（在此处称为每个基元速率）仅在使用一个视区时有效，且未写入 SV_ViewportIndex。

* 如果 SupportsPerVertexShadingRateWithMultipleViewports 帽标记为 true，则每个造成的顶点速率也称为每个基元速率，可用于多个视区。 此外，在这种情况下，可以在将 SV_ViewportIndex 写入时使用。

请参阅 [PFND3D12DDI_RS_SET_SHADING_RATE_0062](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_rs_set_shading_rate_0062) 和 [D3D12DDI_SHADING_RATE_0062](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d12umddi/ne-d3d12umddi-d3d12ddi_shading_rate_0062)。

### <a name="collect-diagnostic-info"></a>收集诊断信息

*收集诊断信息*允许操作系统从图形适配器的驱动程序（包括呈现和显示功能）收集专用数据。 此新功能在 WDDM 2.6 中是必需的。

新的 DDI 应允许操作系统在每次加载驱动程序时收集信息。 当前，操作系统使用微型端口实现的 DxgkDdiCollectDebugInfo 函数来查询驱动程序专用数据，以获取 TDR （超时检测和恢复）相关事例。 由于各种原因，将使用新的 DDI 来收集数据。 需要诊断时，操作系统将调用此 DDI，提供所请求的信息类型。 驱动程序应收集检查问题并将其提交到操作系统的重要信息。 最终将弃用 DxgkDdiCollectDebugInfo，并将其替换为 DxgkDdiCollectDiagnosticInfo。

请参阅 [DXGKDDI_COLLECTDIAGNOSTICINFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_collectdiagnosticinfo)。

### <a name="background-processing"></a>后台处理

后台处理允许用户模式驱动程序表达所需的线程行为，并允许运行时控制/监视它。 用户模式驱动程序将运转后台线程，为线程分配尽量低的优先级，并依赖于 NT 计划程序来确保这些线程不会干扰关键路径线程（一般会成功）。

Api 允许应用调整适合其工作负荷的后台处理量，以及何时执行该操作。

请参阅 [PFND3D12DDI_QUEUEPROCESSINGWORK_CB_0062](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_queueprocessingwork_cb_0062)。

### <a name="driver-hot-update"></a>驱动程序热更新

驱动程序热更新在需要更新 OS 组件时，尽可能减少服务器停机时间。

驱动程序热修补程序用于向内核模式驱动程序应用安全修补程序。 在这种情况下，系统会要求驱动程序保存适配器内存，停止适配器，卸载驱动程序，加载新的驱动程序，然后重新启动适配器。

请参阅[DXGKDDI_SAVEMEMORYFORHOTUPDATE](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkcb_savememoryforhotupdate)和[DXGKDDI_RESTOREMEMORYFORHOTUPDATE](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_restorememoryforhotupdate)。

## <a name="wddm-25"></a>WDDM 2。5

### <a name="tracked-workloads"></a>跟踪的工作负荷

跟踪的工作负荷是一项试验性功能，可更好地控制处理器执行速度与降低功率消耗之间的平衡，直到出现进一步的通知。 已从 Windows 10 版本2003中删除该实现;和不推荐使用，作为安全修补程序的一部分。

### <a name="content-changes"></a>内容更改

| 主题 | 日期 | 说明 |
| --- | --- | --- |
| [用于 HMDs 和专用显示器的 EDID 扩展（VSDB）](specialized-monitors-edid-extension.md) | 12/03/2018 | 显示制造商的规范 |
| [DirectX 图形内核子系统（Dxgkrnl）](directx-graphics-kernel-subsystem.md) | 12/04/2018 | Windows 操作系统通过 Microsoft DirectX 图形内核子系统（Dxgkrnl）实现的内核模式接口。 |
| [WDDM 2.1 功能](wddm-2-1-features.md) | 01/10/2019|介绍 WDDM 2.1 的新增功能和更新功能 |

### <a name="raytracing"></a>Raytracing

为了支持硬件加速的 raytracing，已在 Direct3D API 的并行情况下创建了新的 Direct3D DDI。 示例 DDI 包括：

* [PFND3D12DDI_BUILD_RAYTRACING_ACCELERATION_STRUCTURE_0054](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_build_raytracing_acceleration_structure_0054)
* [PFND3D12DDI_COPY_RAYTRACING_ACCELERATION_STRUCTURE_0054](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_copy_raytracing_acceleration_structure_0054)
* [PFND3D12DDI_EMIT_RAYTRACING_ACCELERATION_STRUCTURE_POSTBUILD_INFO_0054](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_emit_raytracing_acceleration_structure_postbuild_info_0054)
* [PFND3D12DDI_GET_RAYTRACING_ACCELERATION_STRUCTURE_PREBUILD_INFO_0054](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_get_raytracing_acceleration_structure_prebuild_info_0054)

有关 raytracing 的详细信息，请参阅：

* [宣布推出 Microsoft DirectX Raytracing](https://devblogs.microsoft.com/directx/announcing-microsoft-directx-raytracing/)
* [DirectX Raytracing 和 Windows 10 十月2018更新](https://devblogs.microsoft.com/directx/directx-raytracing-and-the-windows-10-october-2018-update/)
* [DirectX 论坛](https://forums.directxtech.com/index.php?topic=5985.0)

### <a name="display-synchronization"></a>显示同步

当驱动程序向操作系统公开显示时，操作系统将检查显示同步的功能，因此在启用显示之前。 对于 TypeIntegratedDisplay 子设备，将通过在适配器初始化期间通过*类型* [DXGKQAITYPE_INTEGRATED_DISPLAY_DESCRIPTOR2](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ne-d3dkmddi-_dxgk_queryadapterinfotype)调用[DxgkDdiQueryAdapterInfo](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_queryadapterinfo)来报告此情况。 对于从 WDDM 2.5 开始受支持的 TypeVideoOutput 子设备，可通过[DxgkDdiUpdateMonitorLinkInfo](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_updatemonitorlinkinfo)将功能作为热插拔处理的一部分进行报告，以便基于目标或连接的监视器来更改功能。

OS 在[DXGK_SET_TIMING_PATH_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_set_timing_path_info#input)结构的每个路径的输入字段的[DxgkDdiSetTimingsFromVidPn](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_settimingsfromvidpn)调用中指定显示同步。

## <a name="wddm-21"></a>WDDM 2。1

WDDM 2.1 启用了新方案，并对 Windows 图形子系统的性能、可靠性、升级复原能力、诊断改进和未来系统改进方面有重大改进。
WDDM 2.0 驱动程序模型是 D3D12 的必备组件。 WDDM 2.0 和 DirectX12 仅适用于 Windows 10 及更高版本。

下面是适用于 WDDM 2.1 的功能添加和更新的列表。

* 通过减少内存管理所用的开销并更有效地使用稀有图形内存，提高了图形性能。 图形性能改进包括：

  * 提供和回收资源-提供和回收改进，以减少后台模式下运行的应用程序的内存占用。
  * 支持2MB 页表条目编码-在 WDDM 2.1 中，已启用 VRAM 中的大型页表项（PTE）编码。 此更改提高了对支持它的系统的性能。
  * 支持64KB 内存页-WDDM 2.1 也支持使用64KB 粒度的虚拟内存分配。 此更改尤其会通过减少访问虚拟内存页面的开销来 Apu 和 Soc。

* 基于*硬件的受*保护内容改进（[PlayReady 3.0](https://docs.microsoft.com/playready/)）

* 图形驱动程序的驱动程序存储区安装，用于改进驱动程序升级复原能力。

* DXIL，一种新的着色器编译器语言

* D3D12 性能和优化改进

* 针对开发人员改进的诊断选项

有关详细信息，请参阅[WDDM 2.1 功能](wddm-2-1-features.md)。

## <a name="wddm-20"></a>WDDM 2。0

WDDM 2.0 包括内存管理更新。

### <a name="gpu-virtual-memory"></a>GPU 虚拟内存

* 所有物理内存都抽象到可由图形处理单元（GPU）内存管理器管理的虚拟段。
* 每个进程都将获取其自己的 GPU 虚拟地址空间。
* 删除了对 swizzling 范围的支持。

有关更多详细信息，请参阅[WDDM 2.0 中的 GPU 虚拟内存](gpu-virtual-memory-in-wddm-2-0.md)。

### <a name="driver-residency"></a>驱动程序驻留

* 在向驱动程序提交命令缓冲区之前，视频内存管理器可确保分配驻留在内存中。 为了便于此功能，已添加了新的用户模式驱动程序设备驱动程序接口（DDIs）（[*MakeResident*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_makeresidentcb)、 [*TrimResidency*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_trimresidencyset)、[*弃用*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_evictcb)）。
* "分配" 和 "修补程序位置" 列表将分阶段出现，因为这在新模型中不是必需的。
* 用户模式驱动程序现在负责处理分配跟踪，还添加了几个新的 DDIs 来实现此操作。
* 驱动程序具有内存预算，并应在内存压力下适应。 这允许通用 Windows 驱动程序跨应用程序平台工作。
* 添加了新的 DDIs，用于处理同步和上下文监视。

有关更多详细信息，请参阅[WDDM 2.0 中的驱动程序驻留](driver-residency-in-wddm-2-0.md)。
