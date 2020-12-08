---
title: Windows 显示驱动程序模型 (WDDM) 操作流
description: Windows 显示驱动程序模型 (WDDM) 操作流
keywords:
- 显示驱动程序模型 WDK Windows Vista，操作流
- Windows Vista 显示器驱动程序模型 WDK，操作流
- 呈现设备 WDK 显示
- 命令缓冲区 WDK 显示，操作流
- DMA 缓冲区 WDK 显示，操作流
- 缓冲 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 74fdc661d3e6bc3060bbd09af129958f8a34d999
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818527"
---
# <a name="windows-display-driver-model-wddm-operation-flow"></a>Windows 显示驱动程序模型 (WDDM) 操作流


下图显示了从创建呈现设备到显示内容时，Windows 显示驱动程序模型 (WDDM) 操作的流。 下面各部分中的序列更详细地介绍了操作流。

![阐释 wddm 操作流的关系图](images/lddmflow.png)

### <a name="span-idcreating_a_rendering_devicespanspan-idcreating_a_rendering_devicespanspan-idcreating_a_rendering_devicespancreating-a-rendering-device"></a><span id="Creating_a_Rendering_Device"></span><span id="creating_a_rendering_device"></span><span id="CREATING_A_RENDERING_DEVICE"></span>创建渲染设备

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>1.</p></td>
<td align="left"><p>在应用程序请求创建呈现设备后，显示微型端口驱动程序将接收 <a href="/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_createdevice" data-raw-source="[&lt;strong&gt;DxgkDdiCreateDevice&lt;/strong&gt;](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_createdevice)"><strong>DxgkDdiCreateDevice</strong></a> 调用。 显示微型端口驱动程序通过返回指向<a href="/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_createdevice" data-raw-source="[&lt;strong&gt;DXGKARG_CREATEDEVICE&lt;/strong&gt;](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_createdevice)"><strong>DXGKARG_CREATEDEVICE</strong></a>结构的<strong>pInfo</strong>成员中的已填充<a href="/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_deviceinfo" data-raw-source="[&lt;strong&gt;DXGK_DEVICEINFO&lt;/strong&gt;](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_deviceinfo)"><strong>DXGK_DEVICEINFO</strong></a>结构的指针，初始化 DMA)  (的直接内存访问。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2.</p></td>
<td align="left"><p>如果对显示微型端口驱动程序的 <a href="/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_createdevice" data-raw-source="[&lt;strong&gt;DxgkDdiCreateDevice&lt;/strong&gt;](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_createdevice)"><strong>DxgkDdiCreateDevice</strong></a> 的调用成功，Microsoft Direct3D 运行时将调用用户模式显示驱动程序的 <a href="/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createdevice" data-raw-source="[&lt;strong&gt;CreateDevice&lt;/strong&gt;](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createdevice)"><strong>CreateDevice</strong></a> 函数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3.</p></td>
<td align="left"><p>在 <a href="/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createdevice" data-raw-source="[&lt;strong&gt;CreateDevice&lt;/strong&gt;](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createdevice)"><strong>CreateDevice</strong></a> 调用中，用户模式显示驱动程序必须显式调用 <a href="/previous-versions/ff568895(v=vs.85)" data-raw-source="[&lt;strong&gt;pfnCreateContextCb&lt;/strong&gt;](/previous-versions/ff568895(v=vs.85))"><strong>pfnCreateContextCb</strong></a> 函数来创建一个或多个上下文，即在新创建的设备上执行的 GPU 线程。 Direct3D 运行时返回<a href="/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddicb_createcontext" data-raw-source="[&lt;strong&gt;D3DDDICB_CREATECONTEXT&lt;/strong&gt;](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddicb_createcontext)"><strong>D3DDDICB_CREATECONTEXT</strong></a>结构的<strong>pCommandBuffer</strong>和<strong>CommandBufferSize</strong>成员中的信息，以初始化命令缓冲区。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idcreating_surfaces_for_a_devicespanspan-idcreating_surfaces_for_a_devicespanspan-idcreating_surfaces_for_a_devicespancreating-surfaces-for-a-device"></a><span id="Creating_Surfaces_for_a_Device"></span><span id="creating_surfaces_for_a_device"></span><span id="CREATING_SURFACES_FOR_A_DEVICE"></span>为设备创建表面

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>4.</p></td>
<td align="left"><p>在应用程序请求为呈现设备创建表面后，Direct3D 运行时将调用用户模式显示驱动程序的 <a href="/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource" data-raw-source="[&lt;strong&gt;CreateResource&lt;/strong&gt;](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource)"><strong>CreateResource</strong></a> 函数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>5.</p></td>
<td align="left"><p>用户模式显示驱动程序的 <a href="/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource" data-raw-source="[&lt;strong&gt;CreateResource&lt;/strong&gt;](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource)"><strong>CreateResource</strong></a> 调用 <a href="/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_allocatecb" data-raw-source="[&lt;strong&gt;pfnAllocateCb&lt;/strong&gt;](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_allocatecb)"><strong>pfnAllocateCb</strong></a> 运行时提供的函数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>6.</p></td>
<td align="left"><p>显示微型端口驱动程序接收 <a href="/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_createallocation" data-raw-source="[&lt;strong&gt;DxgkDdiCreateAllocation&lt;/strong&gt;](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_createallocation)"><strong>DxgkDdiCreateAllocation</strong></a> 调用，指示要创建的分配的数量和类型。 <strong>DxgkDdiCreateAllocation</strong>返回有关<a href="/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_createallocation" data-raw-source="[&lt;strong&gt;DXGKARG_CREATEALLOCATION&lt;/strong&gt;](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_createallocation)"><strong>DXGKARG_CREATEALLOCATION</strong></a>结构的<strong>pAllocationInfo</strong>成员中<a href="/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_allocationinfo" data-raw-source="[&lt;strong&gt;DXGK_ALLOCATIONINFO&lt;/strong&gt;](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_allocationinfo)"><strong>DXGK_ALLOCATIONINFO</strong></a>结构数组中的分配的信息。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idsubmitting_the_command_buffer_to_kernel_modespanspan-idsubmitting_the_command_buffer_to_kernel_modespanspan-idsubmitting_the_command_buffer_to_kernel_modespansubmitting-the-command-buffer-to-kernel-mode"></a><span id="Submitting_the_Command_Buffer_to_Kernel_Mode"></span><span id="submitting_the_command_buffer_to_kernel_mode"></span><span id="SUBMITTING_THE_COMMAND_BUFFER_TO_KERNEL_MODE"></span>向内核模式提交命令缓冲区

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>7.</p></td>
<td align="left"><p>在应用程序请求绘制到图面后，Direct3D 运行时将调用与绘图操作相关的用户模式显示驱动程序函数，例如 <a href="/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_drawprimitive2" data-raw-source="[&lt;strong&gt;DrawPrimitive2&lt;/strong&gt;](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_drawprimitive2)"><strong>DrawPrimitive2</strong></a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>8.</p></td>
<td align="left"><p>若要将命令缓冲区提交到内核模式，Direct3D 运行时需要调用用户模式显示驱动程序的 <a href="/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_present" data-raw-source="[&lt;strong&gt;Present&lt;/strong&gt;](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_present)"><strong>当前</strong></a> 或 <a href="/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_flush" data-raw-source="[&lt;strong&gt;Flush&lt;/strong&gt;](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_flush)"><strong>刷新</strong></a> 函数。 此外，如果命令缓冲区已满，用户模式显示驱动程序将提交命令缓冲区。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>9.</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_present" data-raw-source="[&lt;strong&gt;Present&lt;/strong&gt;](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_present)"><strong>如果调用</strong></a>了 Flush，则用户模式显示驱动程序将调用<a href="/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_presentcb" data-raw-source="[&lt;strong&gt;pfnPresentCb&lt;/strong&gt;](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_presentcb)"><strong>pfnPresentCb</strong></a>运行时提供的函数; 如果调用了<a href="/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_flush" data-raw-source="[&lt;strong&gt;Flush&lt;/strong&gt;](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_flush)"><strong>Flush</strong></a> ，则调用<a href="/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_rendercb" data-raw-source="[&lt;strong&gt;pfnRenderCb&lt;/strong&gt;](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_rendercb)"><strong>pfnRenderCb</strong></a>运行时提供的函数，或者命令缓冲区已满。</p></td>
</tr>
<tr class="even">
<td align="left"><p>10.</p></td>
<td align="left"><p>如果调用了<a href="/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_presentcb" data-raw-source="[&lt;strong&gt;pfnPresentCb&lt;/strong&gt;](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_presentcb)"><strong>pfnPresentCb</strong></a> ，则显示微型端口驱动程序将接收对<a href="/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_present" data-raw-source="[&lt;strong&gt;DxgkDdiPresent&lt;/strong&gt;](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_present)"><strong>DxgkDdiPresent</strong></a>函数的调用，如果调用了<a href="/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_rendercb" data-raw-source="[&lt;strong&gt;pfnRenderCb&lt;/strong&gt;](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_rendercb)"><strong>pfnRenderCb</strong></a> ，则接收<a href="/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_render" data-raw-source="[&lt;strong&gt;DxgkDdiRender&lt;/strong&gt;](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_render)"><strong>DxgkDdiRender</strong></a>或<a href="/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_renderkm" data-raw-source="[&lt;strong&gt;DxgkDdiRenderKm&lt;/strong&gt;](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_renderkm)"><strong>DxgkDdiRenderKm</strong></a>函数。 显示微型端口驱动程序验证命令缓冲区，以硬件的格式写入 DMA 缓冲区，并生成一个描述所使用的表面的分配列表。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idsubmitting_the_dma_buffer_to_hardwarespanspan-idsubmitting_the_dma_buffer_to_hardwarespanspan-idsubmitting_the_dma_buffer_to_hardwarespansubmitting-the-dma-buffer-to-hardware"></a><span id="Submitting_the_DMA_Buffer_to_Hardware"></span><span id="submitting_the_dma_buffer_to_hardware"></span><span id="SUBMITTING_THE_DMA_BUFFER_TO_HARDWARE"></span>将 DMA 缓冲区提交给硬件

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>11.</p></td>
<td align="left"><p>Microsoft DirectX graphics 内核子系统调用显示微型端口驱动程序的 <a href="/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer" data-raw-source="[&lt;strong&gt;DxgkDdiBuildPagingBuffer&lt;/strong&gt;](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer)"><strong>DxgkDdiBuildPagingBuffer</strong></a> 函数来创建特殊用途的 DMA 缓冲区（称为分页缓冲区），该缓冲区将分配列表中指定的分配移到和移出 GPU 可访问的内存。</p>
<div class="alert">
<strong>请注意</strong>，不会为每个帧调用<a href="/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer" data-raw-source="[&lt;strong&gt;DxgkDdiBuildPagingBuffer&lt;/strong&gt;](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer)"><strong>DxgkDdiBuildPagingBuffer</strong></a> 。  
</div>
<div>
 
</div></td>
</tr>
<tr class="even">
<td align="left"><p>12.</p></td>
<td align="left"><p>DirectX 图形内核子系统调用显示微型端口驱动程序的 <a href="/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_submitcommand" data-raw-source="[&lt;strong&gt;DxgkDdiSubmitCommand&lt;/strong&gt;](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_submitcommand)"><strong>DxgkDdiSubmitCommand</strong></a> 函数，以将分页缓冲区排队到 GPU 执行单元中。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>13.</p></td>
<td align="left"><p>DirectX 图形内核子系统调用显示微型端口驱动程序的 <a href="/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_patch" data-raw-source="[&lt;strong&gt;DxgkDdiPatch&lt;/strong&gt;](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_patch)"><strong>DxgkDdiPatch</strong></a> 函数，以将物理地址分配给 DMA 缓冲区中的资源。</p></td>
</tr>
<tr class="even">
<td align="left"><p>14.</p></td>
<td align="left"><p>DirectX 图形内核子系统调用显示微型端口驱动程序的 <a href="/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_submitcommand" data-raw-source="[&lt;strong&gt;DxgkDdiSubmitCommand&lt;/strong&gt;](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_submitcommand)"><strong>DxgkDdiSubmitCommand</strong></a> 函数，将 DMA 缓冲区排队到 GPU 执行单元中。 提交到 GPU 的每个 DMA 缓冲区都包含一个数字的隔离标识符。 GPU 完成处理 DMA 缓冲区后，GPU 将生成一个中断。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>15.</p></td>
<td align="left"><p>显示微型端口驱动程序会在其 <a href="/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_interrupt_routine" data-raw-source="[&lt;strong&gt;DxgkDdiInterruptRoutine&lt;/strong&gt;](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_interrupt_routine)"><strong>DxgkDdiInterruptRoutine</strong></a> 函数中通知中断。 显示微型端口驱动程序应从 GPU 读取刚完成的 DMA 缓冲区的防护标识符。</p></td>
</tr>
<tr class="even">
<td align="left"><p>16.</p></td>
<td align="left"><p>显示微型端口驱动程序应调用 <a href="/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkcb_notify_interrupt" data-raw-source="[&lt;strong&gt;DxgkCbNotifyInterrupt&lt;/strong&gt;](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkcb_notify_interrupt)"><strong>DxgkCbNotifyInterrupt</strong></a> 函数，通知 DirectX 图形内核子系统 DMA 缓冲区已完成。 显示微型端口驱动程序还应调用 <a href="/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkcb_queue_dpc" data-raw-source="[&lt;strong&gt;DxgkCbQueueDpc&lt;/strong&gt;](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkcb_queue_dpc)"><strong>DxgkCbQueueDpc</strong></a> 函数，以便将延迟的过程调用排队 (DPC) 。</p></td>
</tr>
</tbody>
</table>

 

