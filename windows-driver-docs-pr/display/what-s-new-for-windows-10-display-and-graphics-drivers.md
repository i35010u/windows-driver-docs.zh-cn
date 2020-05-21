---
title: Windows 10 显示器和图形驱动程序的新增功能
description: 描述用于显示驱动程序的 Windows 10 中的新增功能
ms.assetid: 619175D4-98DA-4B17-8F6F-71B13A31374D
ms.date: 05/12/2020
ms.localizationpriority: medium
ms.openlocfilehash: 216bfce264256b623630892c85a67fc8fe39d509
ms.sourcegitcommit: d395d4b36f39d3557adda53735a4fdc8745a6408
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2020
ms.locfileid: "83666550"
---
# <a name="whats-new-for-windows-10-display-and-graphics-drivers"></a>Windows 10 显示器和图形驱动程序的新增功能

本页介绍适用于 Windows 10 版本2004（WDDM 2.7）的显示和图形驱动程序中的新增功能。 若要查看在以前版本的 WDDM 2.x 中添加的功能，请参阅[之前的 wddm 2.x 版本的新增](what-s-new-for-prior-wddm-2-x-versions.md)功能。

## <a name="mesh-shaders"></a>网格着色器

网格着色器是在使用光栅化时提高 Direct3D 12 图形管道的灵活性和性能的一种方法。 它们作为输入汇编程序（特别是顶点和几何着色器阶段）的新替代，将一些输入汇编程序的固定函数行为替换为灵活函数的行为。 使用网格着色器，应用程序可以更早、更有效地应用于输入汇编程序。 可以剔除基元，而不是由 GPU 处理索引数据，因为我们看到3D 应用程序的基元计数随着时间的推移越来越高和更高。

如果附加了一个像素着色器，则从网格着色器输出的基元将直接送入 "像素着色器" 阶段。

网格着色器功能引入了网格着色器阶段和新阶段：放大着色器。 Amplifications 着色器替换 GPU 分割阶段。 应用程序将其放大着色器设置为根据需要调用网格着色器若干次。 放大着色器是一个可选步骤，可让应用程序动态控制几何详细信息的级别。

网格着色器功能涉及新的底纹语言构造以及 UMD 的更改。 对于网格着色器的报表设备功能，有一个名为**MeshShaderTier**的字段，通过[**D3D12DDI_D3D12_OPTIONS_DATA_0073**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d12umddi/ns-d3d12umddi-d3d12ddi_d3d12_options_data_0073)报告。 而且，由于这会引入两个新的着色器阶段，因此[**D3D12DDIARG_CREATE_PIPELINE_STATE_0075**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d12umddi/ns-d3d12umddi-d3d12ddiarg_create_pipeline_state_0075)、 **hMeshShader**和**hAmplificationShader**中有两个新字段。 若要启动，请参阅 "DDI [**PFND3D12DDI_DISPATCH_MESH_0074**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_dispatch_mesh_0074)的命令列表" 和 "间接调度[**D3D12DDI_INDIRECT_ARGUMENT_TYPE_DISPATCH_MESH**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d12umddi/ne-d3d12umddi-d3d12ddi_indirect_argument_type) "。

## <a name="directx-raytracing-dxr-11"></a>DirectX Raytracing （DXR）1。1

WDDM 2.7 引入了一些新功能和改进功能，这些功能在 Direct3D 12 中的 DXR 的初始版本上生成。

- Inline raytracing 是 raytracing 的一种替代形式，不使用任何单独的动态着色器或着色器表。 它为开发人员提供灵活性，在所有这些情况下，如果着色器使用 DXR 1.0 样式 raytracing，请将其称为 "基于动态着色器的 raytracing，不适合"。 可在任何着色器阶段（包括计算着色器、像素着色器等）中使用 Inline raytracing。 此处所述的内容可用于 WDDM 2.7，尽管它不对应于 DDI 更改。

- 应用程序可以通过 ExecuteIndirect 调用 DispatchRays，从而允许在 GPU 上配置 raytracing 工作。 对于查找、排序或调整 raytracing 工作的应用程序，以及使用着色器执行此操作，这可能很有用。 接下来，现在有一个 D3D12DDI_INDIRECT_ARGUMENT_TYPE 枚举值。 使用间接 raytracing 调度时，执行间接缓冲区的每个元素都是类型[**D3D12DDIARG_DISPATCH_RAYS_0054**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d12umddi/ns-d3d12umddi-d3d12ddiarg_dispatch_rays_0054)。

- 创建管道状态以用于不同着色器组合的开销是3D 计算机图形中的一项困难问题。 DXR 1.1 包含可帮助的内容：添加到状态对象。 AddToStateObject （）在 API 中公开时，使应用程序能够将着色器添加到具有 CPU 开销的现有状态对象，仅限于添加的内容。 与此一起，有两个设备 DDI 函数： [**PFND3D12DDI_ADD_TO_STATE_OBJECT_0072**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_add_to_state_object_0072)和 PFND3D12DDI_CALC_PRIVATE_ADD_TO_STATE_OBJECT_SIZE_0072 * *] （ https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_calc_private_add_to_state_object_size_0072) 。

对于常规功能报表，有一个新的枚举值[**D3D12DDI_RAYTRACING_TIER_1_1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d12umddi/ne-d3d12umddi-d3d12ddi_raytracing_tier)用于报表层1.1。

## <a name="sampler-feedback"></a>采样器反馈

采样器反馈是一项 Direct3D 12 功能，用于捕获和记录纹理采样信息和位置。 如果没有采样器反馈，则这些详细信息对开发人员是不透明的。 此功能使应用程序不仅可以知道采样了哪些 mip，还能了解在这些 mips 上的位置。 应用程序可能对采样信息感兴趣，例如：

- 准确了解在纹理流式处理系统中接下来要加载的内容，或
- 准确了解需要在纹理空间着色渲染系统中为其着色的内容。

示例操作的反馈会写入 "反馈映射"，它充当一种不透明资源，这类资源必须转码，才能获取 inspectable 的信息。与编写反馈本身一样，着色器模型6_5 中有 HLSL 的构造。 语义非常类似于 Texture2D's 示例及其变体的语义。

虽然取样器反馈可以充分利用新的底纹语言构造，但它也涉及 UMD 的更改。 对于设备功能检查，有一个名为 "SamplerFeedbackTier" 的上限通过[**D3D12DDI_D3D12_OPTIONS_DATA_0073**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d12umddi/ns-d3d12umddi-d3d12ddi_d3d12_options_data_0073)报告。 已将资源创建修改为采用[**D3D12DDI_MIP_REGION_0075**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d12umddi/ns-d3d12umddi-d3d12ddi_mip_region_0075)类型的新字段 "采样器反馈" mip 区域。 与此一起，还有一个新的描述符创建方法， [**PFND3D12DDI_CREATE_SAMPLER_FEEDBACK_UNORDERED_ACCESS_VIEW_0075**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_create_sampler_feedback_unordered_access_view_0075)。

## <a name="content-protection"></a>内容保护

在 WDDM 2.7 中，将可选的受保护资源支持添加到 Direct3D 12 视频操作。 对于后台，受保护的资源已存在于 WDDM 2.7 之前，但仅可用于跨 API 共享和图形或计算，而不能用于视频。

驱动程序不会将对受保护资源的支持作为全局内容进行报告;它基于每个操作。 如果驱动程序报告特定操作支持受保护的资源，则意味着操作可以读取和写入受保护的资源，并支持在资源类型允许的情况下进行跨 API 共享。 值得一提的另一点是，如果驱动程序声明了特定格式的受保护资源支持，则它还必须支持将该格式作为非保护资源。

使用 WDDM 2.7，资源创建方法将被修改为采用可选的 D3D12DDI_HPROTECTEDRESOURCESESSION 实例。 在对象创建时为驱动程序提供此参数，以通知设置和分配。 此外，还会修改内存预算检查以指示该操作是否将使用受保护的资源。 当受保护的资源会话参数为非 NULL 时，这表示该操作将写入受保护的资源。 若要写入未受保护的资源，必须重新创建操作对象。

如果输出是受保护的资源，则解码器和运动估计引用必须是受保护的资源。 在写入受保护资源时，视频处理可能会从受保护和未受保护的资源的组合中进行读取。

在记录写入到受保护资源的一个或多个操作之前，必须使用非 NULL 受保护的资源会话调用[**PFND3D12DDI_SETPROTECTEDRESOURCESESSION_0030**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_setprotectedresourcesession_0030) 。 在记录写入到非保护资源的一个或多个操作之前，需要调用具有 NULL 的**PFND3D12DDI_SETPROTECTEDRESOURCESESSION_0030** 。

若要了解有关 WDDM 2.7 中内容保护的上述第 DDI 更改的指导教程，请参阅[**D3D12DDI_VIDEO_DECODE_PROTECTED_RESOURCES_DATA_0072**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d12umddi/ns-d3d12umddi-d3d12ddi_video_decode_protected_resources_data_0072)作为起点。

## <a name="improved-history-buffer-reporting-for-tools"></a>改进了工具的历史缓冲区报告

WDDM 2.7 引入了 DDI 更改，使 GPU 调试工具可以使用历史缓冲区。 进行此更改后，单个命令缓冲区提交可以包含与多个命令列表对应的工作，而不是一次只包含单个命令列表。 此更改允许 GPU 调试工具更准确地报告应用程序的性能特征。

此功能通过 D3D12DDICAPS_TYPE_0073_SUPPORT_BATCHED_MARKERS 报告。 D3DDDIMLT_BATCHED 存在一个新的枚举值[**D3DDDI_MARKERLOGTYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ne-d3dumddi-d3dddi_markerlogtype) ，这对应于[**D3DDDI_BATCHEDMARKERDATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-d3dddi_batchedmarkerdata)。 当 ETW 事件数据结构的类型为 D3DDDIMLT_BATCHED 时，它已被 revved 为包含若干**D3DDDI_BATCHEDMARKERDATA**元素。

## <a name="displayport-dp-auxi2c"></a>DisplayPort （DP） AUX/I2C

DP 辅助（AUX）通道提供对 DP 配置数据（DPCD）的访问，它是一个每设备注册文件，用于读取 DP 设备的功能、链接定型、拓扑发现、I2C 总线访问等。 请参阅[DXGK_DP_INTERFACE](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/ns-dispmprt-dxgk_dp_interface)作为起点。
