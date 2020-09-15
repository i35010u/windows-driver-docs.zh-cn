---
title: 上下文监视
description: 监视的隔离对象是一种高级的防护防护形式，它允许 CPU 核心或图形处理单元 (GPU) 引擎在特定的防护对象上发出信号或等待，允许在 GPU 引擎之间或跨 CPU 核心和 GPU 引擎进行非常灵活的同步。
ms.assetid: B593FC24-3F8B-4C8A-BBF9-8EF88B748536
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e4364fef87b546dfdf9504c12da94d1eeb219dfd
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90104702"
---
# <a name="context-monitoring"></a>上下文监视


监视的隔离对象是一种高级的防护防护形式，它允许 CPU 核心或图形处理单元 (GPU) 引擎在特定的防护对象上发出信号或等待，允许在 GPU 引擎之间或跨 CPU 核心和 GPU 引擎进行非常灵活的同步。

## <a name="span-id_monitored_fence_creationspanspan-id_monitored_fence_creationspanspan-id_monitored_fence_creationspan-monitored-fence-creation"></a><span id="_Monitored_fence_creation"></span><span id="_monitored_fence_creation"></span><span id="_MONITORED_FENCE_CREATION"></span> 监视的防护创建


受监视的隔离对象是通过使用新的同步对象类型**D3DDDI \_ 监视的 \_ 防护**来调用[*CreateSynchronizationObjectCb*](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createsynchronizationobjectcb)回调创建的。

将创建一个监视的防护对象以及以下属性：

-   初始值
-   标志 (指定其等待和信号行为) 

创建时，图形内核将返回由以下项组成的隔离对象：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Item</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="hSyncObject"></span><span id="hsyncobject"></span><span id="HSYNCOBJECT"></span>hSyncObject</p></td>
<td align="left"><p>同步对象的句柄。 用于在对图形内核的调用中进行引用。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="FenceValueCPUVirtualAddress"></span><span id="fencevaluecpuvirtualaddress"></span><span id="FENCEVALUECPUVIRTUALADDRESS"></span>FenceValueCPUVirtualAddress</p></td>
<td align="left"><p>用于 CPU (64 位) 的防护值的只读映射。 此地址是从支持 i/o 聚合的平台上的 CPU （在其他平台上，UC (未缓存) ）的角度，映射 WB (可缓存的) 。 只需读取此内存位置，即可让 CPU 跟踪围栏进度。 不允许 CPU 写入此内存位置。 若要向该防护发出信号，需要 CPU 来调用 <a href="/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_signalsynchronizationobjectfromcpucb" data-raw-source="[&lt;em&gt;SignalSynchronizationObjectFromCpuCb&lt;/em&gt;](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_signalsynchronizationobjectfromcpucb)"><em>SignalSynchronizationObjectFromCpuCb</em></a>。</p>
<p>支持 <em>IoMmu</em> 的适配器应使用此地址来访问 GPU。 在这种情况下，该地址将映射为读写。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="FenceValueGPUVirtualAddress"></span><span id="fencevaluegpuvirtualaddress"></span><span id="FENCEVALUEGPUVIRTUALADDRESS"></span>FenceValueGPUVirtualAddress</p></td>
<td align="left"><p>GPU (64 位) 的防护值的读取/写入映射。 此地址映射为在支持它的平台上需要 i/o 一致性。 若要向该围栏发出信号，可以使用 GPU 直接写入此 GPU 虚拟地址。</p>
<p><em>IoMmu</em>gpu 不应使用此地址。</p></td>
</tr>
</tbody>
</table>

 

防护值为64位值，其各自的虚拟地址在64位边界上对齐。 Gpu 应声明它们是否可以通过新的 [**DXGK \_ VIDSCHCAPS**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_vidschcaps)：：**No64BitAtomics** 标志以原子方式更新64位值。 如果 GPU 只能以原子方式更新32位值，操作系统会自动处理围栏环绕情况。 不过，它会限制未完成的等待和信号防护值不能比上一个发出的防护值多 **UINT \_ MAX**/2。
## <a name="span-idgpu_signalspanspan-idgpu_signalspanspan-idgpu_signalspangpu-signal"></a><span id="GPU_signal"></span><span id="gpu_signal"></span><span id="GPU_SIGNAL"></span>GPU 信号


如果 GPU 引擎无法使用其虚拟地址写入受监视的防护，则用户模式驱动程序将使用新的 [*SignalSynchronizationObjectFromGpuCb*](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_signalsynchronizationobjectfromgpucb) 回调，该回调会将软件信号数据包排队到 GPU 上下文。

为了向 GPU 发送防护，用户模式驱动程序直接在上下文命令流中插入一个隔离写入命令，而无需经过内核模型。 内核监视围栏进度的机制会有所不同，具体取决于特定的 GPU 引擎是否支持所监视的隔离的基本或高级实现。

当命令缓冲区在 GPU 上完成执行时，图形内核将通过具有挂起等待的防护对象列表，这些对象可在此过程中发出信号，读取其当前的防护值，并确定是否有任何需要取消等待的等待进程。

## <a name="span-id_gpu_waitspanspan-id_gpu_waitspanspan-id_gpu_waitspan-gpu-wait"></a><span id="_GPU_wait"></span><span id="_gpu_wait"></span><span id="_GPU_WAIT"></span> GPU 等待


若要在 GPU 引擎上等待监视的防护，用户模式驱动程序首先需要刷新其挂起的命令缓冲区，然后调用 [*WaitForSynchronizationObjectFromGpuCb*](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_waitforsynchronizationobjectfromgpucb) ，指定 (**hSyncObject**) 的防护对象，以及要等待的防护值。 图形内核会将依赖关系排队到其内部数据库，然后立即返回到用户模式驱动程序，以便它可以继续在等待操作后将工作排队。 在满足等待操作之前，不会计划执行等待操作后提交的命令缓冲区。

## <a name="span-idcpu_signalspanspan-idcpu_signalspanspan-idcpu_signalspancpu-signal"></a><span id="CPU_signal"></span><span id="cpu_signal"></span><span id="CPU_SIGNAL"></span>CPU 信号


添加了新的 [*SignalSynchronizationObjectFromCpuCb*](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_signalsynchronizationobjectfromcpucb) ，以允许 CPU 发出受监视的防护对象的信号。 当 CPU 终止受监视的防护对象时，图形内核将使用发出通知的值更新围栏内存位置，使其立即可供任何用户模式读取器使用，并立即取消任何符合性的等待进程。

## <a name="span-idcpu_waitspanspan-idcpu_waitspanspan-idcpu_waitspancpu-wait"></a><span id="CPU_wait"></span><span id="cpu_wait"></span><span id="CPU_WAIT"></span>CPU 等待


添加了新的 [*WaitForSynchronizationObjectFromCpuCb*](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_waitforsynchronizationobjectfromcpucb) ，以允许 CPU 等待监视的防护对象。 提供两种形式的等待操作。 在第一种形式中， *WaitForSynchronizationObjectFromCpuCb* 回调会阻止，直到满足等待。 在第二种形式中， *WaitForSynchronizationObjectFromCpuCb* 采用一个 CPU 事件句柄，一旦满足等待条件，就会发出信号。

