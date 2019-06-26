---
title: GPU 抢占
description: 可从 Windows 8 开始新的 GPU 抢占模型。
ms.assetid: 9382786E-2E1E-408F-A9E9-04EEEA1CC34A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a3bf94e85471af20e5db953f9d330796f658b138
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379954"
---
# <a name="gpu-preemption"></a>GPU 抢占


可从 Windows 8 开始新的 GPU 抢占模型。 在此模型中操作系统不再允许将抢占 GPU 直接内存访问 (DMA) 数据包被禁用，并且它保证抢占请求，将发送到 GPU 之前[超时检测和恢复 (TDR)](timeout-detection-and-recovery.md)启动过程。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">Windows 显示器驱动程序模型 (WDDM) 的最低版本</td>
<td align="left">1.2</td>
</tr>
<tr class="even">
<td align="left">最大 Windows 版本</td>
<td align="left">8</td>
</tr>
<tr class="odd">
<td align="left">驱动程序实现 — 仅完全图形和呈现</td>
<td align="left">强制</td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit" data-raw-source="[WHCK](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)">WHCK</a>要求和测试</td>
<td align="left"><p><strong>Device.Graphics...抢占测试</strong></p>
<p><strong>Device.Graphics...FlipOnVSyncMmIo</strong></p></td>
</tr>
</tbody>
</table>

 

如果长时间运行的数据包不能成功被抢占，高优先级 GPU 工作，例如所需的桌面窗口管理器 (DWM) 中，工作可能会延迟，在窗口过渡和动画期间导致问题。 此外，不能被抢占的长时间运行 GPU 数据包可能会导致重复重置 GPU，TDR 过程，最终可能发生系统错误检查。

**请注意**  所有 WDDM 1.2 显示微型端口驱动程序必须支持 Windows 8 抢占模型。 但是，当在操作中，WDDM 1.2 驱动程序还可以拒绝 Windows 8 抢占模型，并保留 Windows 7 的 Microsoft DirectX 图形内核子系统计划程序的行为。

 

## <a name="span-idgpupreemptiondevicedriverinterfacesddisspanspan-idgpupreemptiondevicedriverinterfacesddisspanspan-idgpupreemptiondevicedriverinterfacesddisspangpu-preemption-device-driver-interfaces-ddis"></a><span id="GPU_preemption_device_driver_interfaces__DDIs_"></span><span id="gpu_preemption_device_driver_interfaces__ddis_"></span><span id="GPU_PREEMPTION_DEVICE_DRIVER_INTERFACES__DDIS_"></span>GPU 抢占设备驱动程序接口 (DDIs)


以下设备驱动程序接口 (DDIs) 都可用于显示微型端口驱动程序来实现 Windows 8 GPU 抢占模型。

-   [*DxgkCbCreateContextAllocation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkcb_createcontextallocation)
-   [*DxgkCbDestroyContextAllocation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkcb_destroycontextallocation)
-   [*pfnSetPriorityCb*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_setprioritycb)
-   [Dxgkrnl 接口](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)
-   [**DXGKRNL\_INTERFACE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/ns-dispmprt-_dxgkrnl_interface)
-   [**D3DKMDT\_计算\_抢占\_粒度**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ne-d3dkmdt-_d3dkmdt_compute_preemption_granularity)
-   [**D3DKMDT\_图形\_抢占\_粒度**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ne-d3dkmdt-_d3dkmdt_graphics_preemption_granularity)
-   [**D3DKMDT\_抢占\_CAP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ns-d3dkmdt-_d3dkmdt_preemption_caps)
-   [**D3DKMT\_QUERYADAPTERINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/ns-d3dkmthk-_d3dkmt_queryadapterinfo)
-   [**DXGK\_DRIVERCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_drivercaps)
-   [**DXGK\_SUBMITCOMMANDFLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_submitcommandflags)
-   [**DXGK\_VIDSCHCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_vidschcaps)
-   [**DXGKARGCB\_CREATECONTEXTALLOCATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgkargcb_createcontextallocation)

## <a name="span-iddisplayminiportdriverimplementationspanspan-iddisplayminiportdriverimplementationspanspan-iddisplayminiportdriverimplementationspandisplay-miniport-driver-implementation"></a><span id="Display_miniport_driver_implementation"></span><span id="display_miniport_driver_implementation"></span><span id="DISPLAY_MINIPORT_DRIVER_IMPLEMENTATION"></span>显示微型端口驱动程序实现


请按照下列常规步骤以在显示的微型端口驱动程序中实现 Windows 8 GPU 抢占模型：

1.  编译您的驱动程序具有的标头**DXGKDDI\_界面\_版本** &gt; =  **DXGKDDI\_接口\_版本\_WIN8**。
2.  通过设置声明对 Windows 8 GPU 抢占模型的支持**PreemptionAware**并**MultiEngineAware**的成员[ **DXGK\_VIDSCHCAPS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_vidschcaps)结构为 1。 若要支持 Windows 7 抢占模型，将设置**PreemptionAware**为零。
3.  指定支持的级别中的抢占粒度[ **D3DKMDT\_抢占\_CAPS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ns-d3dkmdt-_d3dkmdt_preemption_caps)结构，它接受的常量值从[ **D3DKMDT\_图形\_抢占\_粒度**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ne-d3dkmdt-_d3dkmdt_graphics_preemption_granularity)并[ **D3DKMDT\_计算\_抢占\_粒度**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ne-d3dkmdt-_d3dkmdt_compute_preemption_granularity)枚举。
4.  如果硬件支持延迟上下文切换，提交到的长度为零的缓冲区[ *DxgkDdiSubmitCommand* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_submitcommand)函数，并设置*pSubmitCommand* - &gt;**标志**-&gt;**ContextSwitch**为 1 的成员。 请注意下的讨论**ContextSwitch**的成员[ **DXGK\_SUBMITCOMMANDFLAGS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_submitcommandflags)结构。
5.  通过调用设置 GPU 上下文分配和设备上下文分配[ *DxgkCbCreateContextAllocation* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkcb_createcontextallocation)函数。 请注意的具体说明，为函数提供说明中的限制。
6.  调用[ *DxgkCbDestroyContextAllocation* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkcb_destroycontextallocation)函数来销毁 GPU 上下文分配和使用创建的设备上下文分配[ *DxgkCbCreateContextAllocation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkcb_createcontextallocation)。
7.  准备 DMA 缓冲区，以响应对的调用时[ *DxgkDdiBuildPagingBuffer* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer)函数中，通过填写初始化上下文资源**InitContextResource**中的内部结构[ **DXGKARG\_BUILDPAGINGBUFFER** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgkarg_buildpagingbuffer)结构。 如果在逐出上下文资源或将其重新定位，视频内存管理器将会保留上下文资源的内容。
8.  该驱动程序必须支持内存映射 I/O 翻转下一次垂直同步。在 Windows 8 中，GPU 计划程序尝试抢占硬件，即使投掷处于挂起状态。 因此，若要防止撕裂现象和呈现项目，该驱动程序必须支持内存映射 I/O 翻转模式，必须**FlipOnVSyncMmIo**的成员[ **DXGK\_FLIPCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_flipcaps)结构为 1 并且支持下所述的操作**FlipOnVSyncMmIo**。

### <a name="span-idmemorymappingconsiderationsinyourimplementationspanspan-idmemorymappingconsiderationsinyourimplementationspanspan-idmemorymappingconsiderationsinyourimplementationspanmemory-mapping-considerations-in-your-implementation"></a><span id="Memory_mapping_considerations_in_your_implementation"></span><span id="memory_mapping_considerations_in_your_implementation"></span><span id="MEMORY_MAPPING_CONSIDERATIONS_IN_YOUR_IMPLEMENTATION"></span>在实现中的内存映射注意事项

创建一个可靠的驱动程序，支持 Windows 8 GPU 抢占模型，并按照本指南提供高质量用户体验：

-   DirectX 图形内核 (Dxgkrnl) 计划程序发送抢占命令时，请从 GPU 请求中旬 DMA 缓冲区抢占。 更细的粒度的中旬 DMA 缓冲区抢占的硬件设备应该生成更好的客户体验。
-   允许分页命令隔离 Id 的重复使用： 如果优先的硬件队列中的分页命令导致的抢占请求，计划程序将重新提交的 Dxgkrnl 被抢占分页命令具有相同 fence 最初用于，以及分页的 Id将在该引擎上的任何其他命令之前计划命令。 非分页命令将使用新分配隔离 Id 重新提交。
-   为拆分 DMA 缓冲区提供修补程序位置列表，请参阅[拆分 DMA 缓冲区](splitting-a-dma-buffer.md)。
-   可通过修补程序位置的遍历列表并拒绝的数据包执行解除绑定，或，未对分配的每个拆分数据包称为绑定泄漏检测的验证模式。 有些硬件支持虚拟地址，允许更高级别的可以进行此验证不必要的间接寻址。 在这种情况下，若要指示驱动程序的选择不使用的验证模式，设置**NoDmaPatching**的成员[ **DXGK\_VIDSCHCAPS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_vidschcaps)结构为 1。
-   在 Windows 7 中，计划程序可保证所有对应于相同的拆分 DMA 数据包呈现命令 Dxgkrnl 按顺序执行而无需切换到另一个呈现器上下文。 在 Windows 8 抢占模型中，计划程序可以从对应于相同的呈现命令的两个拆分数据包之间的不同的上下文执行呈现数据包。 因此，可识别的抢占的驱动程序应为正则是完整数据包提交相同的方式处理拆分/部分 DMA 数据包提交。 具体而言，GPU 状态必须保存或还原此类提交的边界上。
-   广播到多个链接的显示适配器 (LDA) 模式下，其中多个物理 Gpu 链接以形成单个，更快，适配器虚拟 GPU 时，抢占感知的驱动程序不得更改拆分 DMA 缓冲区的内容。 这是因为在 Windows 8 抢占模型中，Dxgkrnl 计划程序无法再保证同步执行拆分数据包序列而无需切换到另一个上下文。 更改拆分 DMA 数据包的内容的驱动程序将降低数据包的数据的完整性，因为另一个引擎上执行数据包时，它将运行 DMA 缓冲区数据的相同副本。
-   在 Windows 8 GPU 抢占模型中，Dxgkrnl 计划程序使具有关联的"上的信号提交"同步基元的数据包的抢占。 如果设备使用"上的信号提交"结合使用基于硬件的同步基元等待状态，则它必须支持抢占等待指令，等待条件得到满足之前的功能。

## <a name="span-idhardwarecertificationrequirementsspanspan-idhardwarecertificationrequirementsspanspan-idhardwarecertificationrequirementsspanhardware-certification-requirements"></a><span id="Hardware_certification_requirements"></span><span id="hardware_certification_requirements"></span><span id="HARDWARE_CERTIFICATION_REQUIREMENTS"></span>硬件认证要求


有关实现此功能时，必须满足硬件设备要求的信息，请参阅相关[WHCK 文档](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)上**Device.Graphics...抢占测试**和**Device.Graphics...FlipOnVSyncMmIo**。

请参阅[WDDM 1.2 功能](wddm-v1-2-features.md)评审的 Windows 8 一起添加的功能。

 

 





