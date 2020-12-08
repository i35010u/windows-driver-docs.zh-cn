---
title: GPU 抢占
description: 从 Windows 8 开始，可以使用新的 GPU 抢占模式。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 33c09d923468089867d2a2c8456ec66e1b98c81c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825759"
---
# <a name="gpu-preemption"></a>GPU 抢占


从 Windows 8 开始，可以使用新的 GPU 抢占模式。 在此模型中，操作系统不再允许对 GPU 直接内存访问进行抢占 (DMA) 要禁用的数据包，并且保证在启动 [超时检测和恢复 (TDR) ](timeout-detection-and-recovery.md) 进程之前将抢占请求发送到 GPU。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">最小 Windows 显示器驱动程序模型 (WDDM) 版本</td>
<td align="left">1.2</td>
</tr>
<tr class="even">
<td align="left">最大 Windows 版本</td>
<td align="left">8</td>
</tr>
<tr class="odd">
<td align="left">驱动程序实现-仅限完整图形和呈现</td>
<td align="left">必需</td>
</tr>
<tr class="even">
<td align="left"><a href="/windows-hardware/test/hlk/windows-hardware-lab-kit" data-raw-source="[WHCK](/windows-hardware/test/hlk/windows-hardware-lab-kit)">WHCK</a> 要求和测试</td>
<td align="left"><p><strong>设备 .。。抢占测试</strong></p>
<p><strong>设备 .。。FlipOnVSyncMmIo</strong></p></td>
</tr>
</tbody>
</table>

 

如果长时间运行的数据包无法成功被抢占，则高优先级 GPU 工作（例如桌面窗口管理器 (DWM) 所需的工作）可能会延迟，从而导致在窗口转换和动画过程中出现故障。 而且，不能被抢占的长时间运行的 GPU 数据包可能会导致 TDR 进程重复重置 GPU，最终可能会发生系统错误检测。

**注意**  
所有 WDDM 1.2 显示微型端口驱动程序都必须支持 Windows 8 抢占模式。 但在操作中，WDDM 1.2 驱动程序还可以拒绝 Windows 8 抢占模型，并保留 Microsoft DirectX 图形内核子系统计划程序的 Windows 7 行为。

 

## <a name="span-idgpu_preemption_device_driver_interfaces__ddis_spanspan-idgpu_preemption_device_driver_interfaces__ddis_spanspan-idgpu_preemption_device_driver_interfaces__ddis_spangpu-preemption-device-driver-interfaces-ddis"></a><span id="GPU_preemption_device_driver_interfaces__DDIs_"></span><span id="gpu_preemption_device_driver_interfaces__ddis_"></span><span id="GPU_PREEMPTION_DEVICE_DRIVER_INTERFACES__DDIS_"></span>GPU 抢占设备驱动程序接口 (DDIs) 


以下设备驱动程序接口 (DDIs) 可用于显示小型端口驱动程序以实现 Windows 8 GPU 抢占模型。

-   [*DxgkCbCreateContextAllocation*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkcb_createcontextallocation)
-   [*DxgkCbDestroyContextAllocation*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkcb_destroycontextallocation)
-   [*pfnSetPriorityCb*](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_setprioritycb)
-   [Dxgkrnl 接口](/windows-hardware/drivers/ddi/index)
-   [**DXGKRNL \_ 接口**](/windows-hardware/drivers/ddi/dispmprt/ns-dispmprt-_dxgkrnl_interface)
-   [**D3DKMDT \_ 计算 \_ 抢占 \_ 粒度**](/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_d3dkmdt_compute_preemption_granularity)
-   [**D3DKMDT \_ 图形 \_ 抢占 \_ 粒度**](/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_d3dkmdt_graphics_preemption_granularity)
-   [**D3DKMDT \_ 抢占 \_ 上限**](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_preemption_caps)
-   [**D3DKMT \_ QUERYADAPTERINFO**](/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_queryadapterinfo)
-   [**DXGK \_ DRIVERCAPS**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_drivercaps)
-   [**DXGK \_ SUBMITCOMMANDFLAGS**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_submitcommandflags)
-   [**DXGK \_ VIDSCHCAPS**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_vidschcaps)
-   [**DXGKARGCB \_ CREATECONTEXTALLOCATION**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkargcb_createcontextallocation)

## <a name="span-iddisplay_miniport_driver_implementationspanspan-iddisplay_miniport_driver_implementationspanspan-iddisplay_miniport_driver_implementationspandisplay-miniport-driver-implementation"></a><span id="Display_miniport_driver_implementation"></span><span id="display_miniport_driver_implementation"></span><span id="DISPLAY_MINIPORT_DRIVER_IMPLEMENTATION"></span>显示微型端口驱动程序实现


请按照以下常规步骤在显示微型端口驱动程序中实现 Windows 8 GPU 抢占模型：

1.  针对具有 **DXGKDDI \_ 接口 \_ 版本** &gt; =  **DXGKDDI \_ 接口 \_ 版本 \_ WIN8** 的标头编译驱动程序。
2.  通过将 [**DXGK \_ VIDSCHCAPS**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_vidschcaps)结构的 **PreemptionAware** 和 **MultiEngineAware** 成员设置为1，声明对 Windows 8 GPU 抢占模型的支持。 若要支持 Windows 7 抢占模型，请将 **PreemptionAware** 设置为零。
3.  在 [**D3DKMDT \_ 抢占 \_ cap**](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_preemption_caps) 结构中指定支持的抢占粒度级别，该结构采用 [**D3DKMDT \_ 图形 \_ 抢占 \_ 粒度**](/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_d3dkmdt_graphics_preemption_granularity) 和 [**D3DKMDT \_ 计算 \_ 抢占 \_ 粒度**](/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_d3dkmdt_compute_preemption_granularity) 枚举中的常量值。
4.  如果硬件支持迟缓上下文切换，请将长度为零的缓冲区提交给 [*DxgkDdiSubmitCommand*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_submitcommand)函数，并将 *pSubmitCommand* - &gt; **标志** - &gt; **ContextSwitch** 成员设置为1。 请注意 [**DXGK \_ SUBMITCOMMANDFLAGS**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_submitcommandflags)结构的 **ContextSwitch** 成员下的讨论。
5.  通过调用 [*DxgkCbCreateContextAllocation*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkcb_createcontextallocation) 函数设置 GPU 上下文分配和设备上下文分配。 请注意该函数的 "备注" 中提供的特定说明和限制。
6.  调用 [*DxgkCbDestroyContextAllocation*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkcb_destroycontextallocation) 函数以销毁通过 [*DXGKCBCREATECONTEXTALLOCATION*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkcb_createcontextallocation)创建的 GPU 上下文分配和设备上下文分配。
7.  在为响应对 [*DxgkDdiBuildPagingBuffer*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer)函数的调用而准备 DMA 缓冲区时，通过在 [**DXGKARG \_ BUILDPAGINGBUFFER**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_buildpagingbuffer)结构中填充 **InitContextResource** 内部结构来初始化上下文资源。 如果逐出或重定位了上下文资源，视频内存管理器将保留上下文资源的内容。
8.  驱动程序必须支持在下一次垂直同步时进行内存映射 i/o 翻转。在 Windows 8 中，GPU 计划程序会尝试抢占硬件，即使翻转处于挂起状态也是如此。 因此，为了防止撕裂和渲染项目，驱动程序必须支持内存映射 i/o 翻转模型，并且必须将 [**DXGK \_ FLIPCAPS**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_flipcaps)结构的 **FlipOnVSyncMmIo** 成员设置为1，并支持 **FlipOnVSyncMmIo** 下所述的操作。

### <a name="span-idmemory_mapping_considerations_in_your_implementationspanspan-idmemory_mapping_considerations_in_your_implementationspanspan-idmemory_mapping_considerations_in_your_implementationspanmemory-mapping-considerations-in-your-implementation"></a><span id="Memory_mapping_considerations_in_your_implementation"></span><span id="memory_mapping_considerations_in_your_implementation"></span><span id="MEMORY_MAPPING_CONSIDERATIONS_IN_YOUR_IMPLEMENTATION"></span>实现中的内存映射注意事项

创建支持 Windows 8 GPU 抢占模型的可靠的驱动程序，并按以下指南提供高质量的用户体验：

-   在 DirectX 图形内核 (Dxgkrnl) 计划程序发送抢占命令时，从 GPU 请求中间 DMA 缓冲区抢占。 具有更精细的中间 DMA 缓冲区抢占的硬件设备应能产生更好的客户体验。
-   允许重新使用寻呼命令隔离 Id：如果抢占请求导致硬件队列中的抢占页面命令，则 Dxgkrnl 计划程序将使用原来用于它们的相同围栏 Id 重新提交已抢占的寻呼命令，并在该引擎上的任何其他命令之前安排分页命令。 将通过新分配的防护 Id 重新提交非分页命令。
-   为拆分 DMA 缓冲区提供修补程序位置列表-请参阅 [拆分 Dma 缓冲区](splitting-a-dma-buffer.md)。
-   验证模式称为绑定泄漏检测，可用于遍历修补程序位置列表并拒绝未取消绑定的数据包，或者不重新编程每个拆分数据包的分配。 某些硬件支持虚拟地址，从而允许额外的间接寻址级别，从而无需进行此验证。 在这种情况下，若要指示驱动程序从验证模式中弹出，请将 [**DXGK \_ VIDSCHCAPS**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_vidschcaps)结构的 **NoDmaPatching** 成员设置为1。
-   在 Windows 7 中，Dxgkrnl 计划程序保证所有对应于同一个 render 命令的拆分 DMA 数据包都按顺序执行，而不会切换到另一个呈现上下文。 在 Windows 8 抢占模型中，计划程序可以在两个对应于同一个 render 命令的拆分数据包之间从不同的上下文执行呈现数据包。 因此，识别抢占的驱动程序应以与常规完整数据包提交相同的方式处理拆分/部分 DMA 数据包提交。 具体而言，必须在此类提交的边界上保存或还原 GPU 状态。
-   如果识别识别的驱动程序在链接的显示适配器中广播到多个适配器，则不能更改拆分 DMA 缓冲区的内容 (LDA) 模式，在该模式下，多个物理 Gpu 链接起来形成一个速度更快的虚拟 GPU。 这是因为，在 Windows 8 抢占模型中，Dxgkrnl 计划程序不再保证拆分数据包序列的同步执行，而不会切换到另一个上下文。 更改了拆分 DMA 数据包的内容的驱动程序会损害数据包数据的完整性，因为如果在另一个引擎上执行了数据包，则会在 DMA 缓冲区数据的相同副本上操作。
-   在 Windows 8 GPU 抢占模型中，Dxgkrnl 计划程序为具有关联的 "提交时的信号" 同步基元的数据包启用抢占。 如果设备在与基于硬件的等待状态结合使用 "提交时发出信号" 同步基元，则它必须支持在满足等待条件之前抢占等待指令的功能。

## <a name="span-idhardware_certification_requirementsspanspan-idhardware_certification_requirementsspanspan-idhardware_certification_requirementsspanhardware-certification-requirements"></a><span id="Hardware_certification_requirements"></span><span id="hardware_certification_requirements"></span><span id="HARDWARE_CERTIFICATION_REQUIREMENTS"></span>硬件认证要求


有关硬件设备实现此功能时必须满足的要求的信息，请参阅相关 [WHCK 文档](/windows-hardware/test/hlk/windows-hardware-lab-kit) **抢占测试** 和 **设备 .。。FlipOnVSyncMmIo**。

请参阅 [WDDM 1.2 功能](wddm-v1-2-features.md) ，了解 Windows 8 中添加的功能。

