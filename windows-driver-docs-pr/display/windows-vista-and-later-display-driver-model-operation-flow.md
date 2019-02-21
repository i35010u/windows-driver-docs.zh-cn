---
title: Windows 显示驱动程序模型 (WDDM) 操作流
description: Windows 显示驱动程序模型 (WDDM) 操作流
ms.assetid: 8d2af92c-392a-457d-af9f-796e1050031d
keywords:
- 显示器驱动程序模型 WDK Windows Vista 中，操作流
- Windows Vista 显示器驱动程序模型 WDK，操作流
- 呈现的设备 WDK 显示
- 命令缓冲区 WDK 显示，操作流
- DMA 缓冲区 WDK 显示，操作流
- 缓冲 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d65ffda8c4276598c2221cb9c5ef845ab8538ff9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525564"
---
# <a name="windows-display-driver-model-wddm-operation-flow"></a>Windows 显示驱动程序模型 (WDDM) 操作流


下图显示了 Windows 显示驱动程序模型 (WDDM) 时呈现设备从创建到的内容显示到显示屏中发生的操作的流。 序列中后面的部分介绍了更多详细信息中的操作流。

![说明 wddm 操作流的关系图](images/lddmflow.png)

### <a name="span-idcreatingarenderingdevicespanspan-idcreatingarenderingdevicespanspan-idcreatingarenderingdevicespancreating-a-rendering-device"></a><span id="Creating_a_Rendering_Device"></span><span id="creating_a_rendering_device"></span><span id="CREATING_A_RENDERING_DEVICE"></span>创建一个渲染设备

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>1.</p></td>
<td align="left"><p>若要创建一个渲染设备的应用程序请求后，将显示微型端口驱动程序收到<a href="https://msdn.microsoft.com/library/windows/hardware/ff559615" data-raw-source="[&lt;strong&gt;DxgkDdiCreateDevice&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559615)"> <strong>DxgkDdiCreateDevice</strong> </a>调用。 显示微型端口驱动程序初始化直接内存访问 (DMA) 通过将指针返回到已填充<a href="https://msdn.microsoft.com/library/windows/hardware/ff561047" data-raw-source="[&lt;strong&gt;DXGK_DEVICEINFO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561047)"> <strong>DXGK_DEVICEINFO</strong> </a>结构<strong>pInfo</strong> 的成员<a href="https://msdn.microsoft.com/library/windows/hardware/ff557570" data-raw-source="[&lt;strong&gt;DXGKARG_CREATEDEVICE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557570)"><strong>DXGKARG_CREATEDEVICE</strong> </a>结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2.</p></td>
<td align="left"><p>如果显示微型端口驱动程序调用&#39;s <a href="https://msdn.microsoft.com/library/windows/hardware/ff559615" data-raw-source="[&lt;strong&gt;DxgkDdiCreateDevice&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559615)"> <strong>DxgkDdiCreateDevice</strong> </a>成功，Microsoft Direct3D 运行时将调用用户模式显示驱动程序&#39;s <a href="https://msdn.microsoft.com/library/windows/hardware/ff540634" data-raw-source="[&lt;strong&gt;CreateDevice&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540634)"> <strong>CreateDevice</strong> </a>函数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3.</p></td>
<td align="left"><p>在中<a href="https://msdn.microsoft.com/library/windows/hardware/ff540634" data-raw-source="[&lt;strong&gt;CreateDevice&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540634)"> <strong>CreateDevice</strong> </a>调用时，用户模式显示驱动程序必须显式调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff568895" data-raw-source="[&lt;strong&gt;pfnCreateContextCb&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568895)"> <strong>pfnCreateContextCb</strong> </a>函数来创建一个或多个上下文 — 新创建的设备上的执行 GPU 线程。 Direct3D 运行时将返回中的信息<strong>pCommandBuffer</strong>并<strong>CommandBufferSize</strong>的成员<a href="https://msdn.microsoft.com/library/windows/hardware/ff544143" data-raw-source="[&lt;strong&gt;D3DDDICB_CREATECONTEXT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544143)"> <strong>D3DDDICB_CREATECONTEXT</strong> </a>结构初始化命令缓冲区。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idcreatingsurfacesforadevicespanspan-idcreatingsurfacesforadevicespanspan-idcreatingsurfacesforadevicespancreating-surfaces-for-a-device"></a><span id="Creating_Surfaces_for_a_Device"></span><span id="creating_surfaces_for_a_device"></span><span id="CREATING_SURFACES_FOR_A_DEVICE"></span>为设备创建图面

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>4.</p></td>
<td align="left"><p>Direct3D 运行时应用程序请求创建设计面的呈现设备后，调用用户模式显示驱动程序&#39;s <a href="https://msdn.microsoft.com/library/windows/hardware/ff540688" data-raw-source="[&lt;strong&gt;CreateResource&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540688)"> <strong>CreateResource</strong> </a>函数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>5.</p></td>
<td align="left"><p>用户模式显示驱动程序&#39;s <a href="https://msdn.microsoft.com/library/windows/hardware/ff540688" data-raw-source="[&lt;strong&gt;CreateResource&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540688)"> <strong>CreateResource</strong> </a>调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff568893" data-raw-source="[&lt;strong&gt;pfnAllocateCb&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568893)"> <strong>pfnAllocateCb</strong> </a>运行时提供的函数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>6.</p></td>
<td align="left"><p>显示微型端口驱动程序收到<a href="https://msdn.microsoft.com/library/windows/hardware/ff559606" data-raw-source="[&lt;strong&gt;DxgkDdiCreateAllocation&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559606)"> <strong>DxgkDdiCreateAllocation</strong> </a>调用，指示要创建的数量和类型的分配。 <strong>DxgkDdiCreateAllocation</strong>的数组中返回有关分配的信息<a href="https://msdn.microsoft.com/library/windows/hardware/ff560960" data-raw-source="[&lt;strong&gt;DXGK_ALLOCATIONINFO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff560960)"> <strong>DXGK_ALLOCATIONINFO</strong> </a>中结构<strong>pAllocationInfo</strong>成员<a href="https://msdn.microsoft.com/library/windows/hardware/ff557559" data-raw-source="[&lt;strong&gt;DXGKARG_CREATEALLOCATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557559)"> <strong>DXGKARG_CREATEALLOCATION</strong> </a>结构。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idsubmittingthecommandbuffertokernelmodespanspan-idsubmittingthecommandbuffertokernelmodespanspan-idsubmittingthecommandbuffertokernelmodespansubmitting-the-command-buffer-to-kernel-mode"></a><span id="Submitting_the_Command_Buffer_to_Kernel_Mode"></span><span id="submitting_the_command_buffer_to_kernel_mode"></span><span id="SUBMITTING_THE_COMMAND_BUFFER_TO_KERNEL_MODE"></span>提交到内核模式的命令缓冲区

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>7.</p></td>
<td align="left"><p>Direct3D 的运行时调用用户模式应用程序请求要绘制到图面后，显示驱动程序函数与绘制操作，例如，相关<a href="https://msdn.microsoft.com/library/windows/hardware/ff556151" data-raw-source="[&lt;strong&gt;DrawPrimitive2&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556151)"> <strong>DrawPrimitive2</strong></a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>8.</p></td>
<td align="left"><p>若要提交到内核模式的命令缓冲区，Direct3D 运行时将调用任一用户模式显示驱动程序&#39;s <a href="https://msdn.microsoft.com/library/windows/hardware/ff569176" data-raw-source="[&lt;strong&gt;Present&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff569176)"><strong>存在</strong></a>或<a href="https://msdn.microsoft.com/library/windows/hardware/ff565957" data-raw-source="[&lt;strong&gt;Flush&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565957)"><strong>刷新</strong></a>函数。 此外，用户模式显示驱动程序提交的命令缓冲区时，如果命令缓冲区已满。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>9.</p></td>
<td align="left"><p>用户模式显示驱动程序调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff568916" data-raw-source="[&lt;strong&gt;pfnPresentCb&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568916)"> <strong>pfnPresentCb</strong> </a>运行时提供的函数如果<a href="https://msdn.microsoft.com/library/windows/hardware/ff569176" data-raw-source="[&lt;strong&gt;Present&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff569176)"><strong>存在</strong></a>调用，或<a href="https://msdn.microsoft.com/library/windows/hardware/ff568923" data-raw-source="[&lt;strong&gt;pfnRenderCb&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568923)"> <strong>pfnRenderCb</strong> </a>运行时提供的函数如果<a href="https://msdn.microsoft.com/library/windows/hardware/ff565957" data-raw-source="[&lt;strong&gt;Flush&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565957)"><strong>刷新</strong></a>调用或命令缓冲区已满。</p></td>
</tr>
<tr class="even">
<td align="left"><p>10.</p></td>
<td align="left"><p>显示微型端口驱动程序接收到调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff559743" data-raw-source="[&lt;strong&gt;DxgkDdiPresent&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559743)"> <strong>DxgkDdiPresent</strong> </a>函数如果<a href="https://msdn.microsoft.com/library/windows/hardware/ff568916" data-raw-source="[&lt;strong&gt;pfnPresentCb&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568916)"> <strong>pfnPresentCb</strong> </a>调用，或<a href="https://msdn.microsoft.com/library/windows/hardware/ff559793" data-raw-source="[&lt;strong&gt;DxgkDdiRender&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559793)"> <strong>DxgkDdiRender</strong> </a>或<a href="https://msdn.microsoft.com/library/windows/hardware/ff559800" data-raw-source="[&lt;strong&gt;DxgkDdiRenderKm&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559800)"> <strong>DxgkDdiRenderKm</strong> </a>函数如果<a href="https://msdn.microsoft.com/library/windows/hardware/ff568923" data-raw-source="[&lt;strong&gt;pfnRenderCb&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568923)"> <strong>pfnRenderCb</strong></a>调用。 显示微型端口驱动程序来验证命令缓冲区，将写入到的硬件中的 DMA 缓冲区&#39;s 格式，并生成使用描述图面分配列表。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idsubmittingthedmabuffertohardwarespanspan-idsubmittingthedmabuffertohardwarespanspan-idsubmittingthedmabuffertohardwarespansubmitting-the-dma-buffer-to-hardware"></a><span id="Submitting_the_DMA_Buffer_to_Hardware"></span><span id="submitting_the_dma_buffer_to_hardware"></span><span id="SUBMITTING_THE_DMA_BUFFER_TO_HARDWARE"></span>提交到硬件的 DMA 缓冲区

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>11.</p></td>
<td align="left"><p>Microsoft DirectX 图形内核子系统调用显示微型端口驱动程序&#39;s <a href="https://msdn.microsoft.com/library/windows/hardware/ff559587" data-raw-source="[&lt;strong&gt;DxgkDdiBuildPagingBuffer&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559587)"> <strong>DxgkDdiBuildPagingBuffer</strong> </a>函数来创建特殊用途的 DMA 缓冲区，称为分页缓冲区移动到和从 GPU 可访问的内存分配列表中指定的分配的。</p>
<div class="alert">
<strong>请注意</strong><a href="https://msdn.microsoft.com/library/windows/hardware/ff559587" data-raw-source="[&lt;strong&gt;DxgkDdiBuildPagingBuffer&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559587)"><strong>DxgkDdiBuildPagingBuffer</strong> </a>不会为每个帧调用。  
</div>
<div>
 
</div></td>
</tr>
<tr class="even">
<td align="left"><p>12.</p></td>
<td align="left"><p>DirectX 图形内核子系统调用显示微型端口驱动程序&#39;s <a href="https://msdn.microsoft.com/library/windows/hardware/ff560790" data-raw-source="[&lt;strong&gt;DxgkDdiSubmitCommand&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff560790)"> <strong>DxgkDdiSubmitCommand</strong> </a>函数进行排队到 GPU 执行单元的分页缓冲区。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>13.</p></td>
<td align="left"><p>DirectX 图形内核子系统调用显示微型端口驱动程序&#39;s <a href="https://msdn.microsoft.com/library/windows/hardware/ff559737" data-raw-source="[&lt;strong&gt;DxgkDdiPatch&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559737)"> <strong>DxgkDdiPatch</strong> </a>函数来将物理地址分配给 DMA 缓冲区中的资源。</p></td>
</tr>
<tr class="even">
<td align="left"><p>14.</p></td>
<td align="left"><p>DirectX 图形内核子系统调用显示微型端口驱动程序&#39;s <a href="https://msdn.microsoft.com/library/windows/hardware/ff560790" data-raw-source="[&lt;strong&gt;DxgkDdiSubmitCommand&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff560790)"> <strong>DxgkDdiSubmitCommand</strong> </a>函数进行排队到 GPU 执行单元的 DMA 缓冲区。 每个提交至 GPU 的 DMA 缓冲区包含 fence 标识符，它是一个数字。 GPU 完成处理的 DMA 缓冲区后，GPU 会产生中断。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>15.</p></td>
<td align="left"><p>在中断的通知显示微型端口驱动程序及其<a href="https://msdn.microsoft.com/library/windows/hardware/ff559680" data-raw-source="[&lt;strong&gt;DxgkDdiInterruptRoutine&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559680)"> <strong>DxgkDdiInterruptRoutine</strong> </a>函数。 显示微型端口驱动程序应显示为从 GPU，刚刚完成的 DMA 缓冲区的 fence 标识符。</p></td>
</tr>
<tr class="even">
<td align="left"><p>16.</p></td>
<td align="left"><p>显示微型端口驱动程序应调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff559545" data-raw-source="[&lt;strong&gt;DxgkCbNotifyInterrupt&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559545)"> <strong>DxgkCbNotifyInterrupt</strong> </a>函数，以通知 DMA 缓冲区已完成的 DirectX 图形内核子系统。 显示微型端口驱动程序还应调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff559559" data-raw-source="[&lt;strong&gt;DxgkCbQueueDpc&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559559)"> <strong>DxgkCbQueueDpc</strong> </a>排队延缓的过程调用 (DPC) 的函数。</p></td>
</tr>
</tbody>
</table>

 

 

 





