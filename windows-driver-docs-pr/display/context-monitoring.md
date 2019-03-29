---
title: 上下文监视
description: 受监视的隔离对象是 fence 同步这将允许 CPU 内核或的图形处理单元 (GPU) 引擎发出信号或等待特定隔离对象，从而允许非常灵活同步 GPU 引擎之间或跨高级窗体CPU 核心数和 GPU 引擎。
ms.assetid: B593FC24-3F8B-4C8A-BBF9-8EF88B748536
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ed9c5aa9b0766e00e3a59ad11711157f75ed70ce
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576359"
---
# <a name="context-monitoring"></a>上下文监视


受监视的隔离对象是 fence 同步这将允许 CPU 内核或的图形处理单元 (GPU) 引擎发出信号或等待特定隔离对象，从而允许非常灵活同步 GPU 引擎之间或跨高级窗体CPU 核心数和 GPU 引擎。

## <a name="span-idmonitoredfencecreationspanspan-idmonitoredfencecreationspanspan-idmonitoredfencecreationspan-monitored-fence-creation"></a><span id="_Monitored_fence_creation"></span><span id="_monitored_fence_creation"></span><span id="_MONITORED_FENCE_CREATION"></span> 受监视的 fence 创建


通过调用创建一个受监视的隔离对象[ *CreateSynchronizationObjectCb* ](https://msdn.microsoft.com/library/windows/hardware/ff568897)具有新的同步对象类型回调**D3DDDI\_MONITORED\_FENCE**。

以及以下属性创建一个受监视的隔离对象：

-   初始值
-   标志 （指定其等待和信号行为）

创建后，图形内核返回以下项组成一个 fence 对象：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">项目</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="hSyncObject"></span><span id="hsyncobject"></span><span id="HSYNCOBJECT"></span>hSyncObject</p></td>
<td align="left"><p>同步对象的句柄。 用于对图形内核的调用中引用它。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="FenceValueCPUVirtualAddress"></span><span id="fencevaluecpuvirtualaddress"></span><span id="FENCEVALUECPUVIRTUALADDRESS"></span>FenceValueCPUVirtualAddress</p></td>
<td align="left"><p>只读映射的围栏值 （64 位） 的 cpu。 此地址映射 WB （缓存） 从角度来看支持 I/O 一致性，UC （未缓存） 在其他平台上的平台上的 cpu。 使 CPU 可以跟踪的围栏进度方法只需读取此内存位置。 CPU 不允许将写入此内存位置。 若要发出信号 fence，CPU 需要先调用<a href="https://msdn.microsoft.com/library/windows/hardware/dn906360" data-raw-source="[&lt;em&gt;SignalSynchronizationObjectFromCpuCb&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/dn906360)"> <em>SignalSynchronizationObjectFromCpuCb</em></a>。</p>
<p>支持的适配器<em>IoMmu</em>应该将此地址用于 GPU 访问权限。 将地址在这种情况下映射为可读写。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="FenceValueGPUVirtualAddress"></span><span id="fencevaluegpuvirtualaddress"></span><span id="FENCEVALUEGPUVIRTUALADDRESS"></span>FenceValueGPUVirtualAddress</p></td>
<td align="left"><p>读/写 GPU 的围栏值 （64 位） 的映射。 此地址映射为所需支持它的平台上的 I/O 一致性。 能够通知 fence，GPU 被可以直接写入此 GPU 虚拟地址。</p>
<p>此地址不应由<em>IoMmu</em>Gpu。</p></td>
</tr>
</tbody>
</table>

 

围栏值为具有 64 位边界上对齐其各自的虚拟地址的 64 位值。 Gpu 应声明它们是否能够以原子方式更新由通过一个新 CPU 的 64 位值为可见[ **DXGK\_VIDSCHCAPS**](https://msdn.microsoft.com/library/windows/hardware/ff562863)::**No64BitAtomics**标志。 如果 GPU 能够仅以原子方式更新 32 位值，操作系统会自动处理 fence 回绕情况。 但是，它会将一个限制，未完成的等待和信号的围栏值不能为多个**UINT\_最大**  /2 从最后一个已发出信号的围栏值。
## <a name="span-idgpusignalspanspan-idgpusignalspanspan-idgpusignalspangpu-signal"></a><span id="GPU_signal"></span><span id="gpu_signal"></span><span id="GPU_SIGNAL"></span>GPU 信号


如果 GPU 引擎不能对受监视的围墙使用其虚拟地址的写入，用户模式驱动程序将使用一个新[ *SignalSynchronizationObjectFromGpuCb* ](https://msdn.microsoft.com/library/windows/hardware/dn906362)将排队的回调软件到 GPU 上下文信号数据包。

能够从 GPU 通知 fence，用户模式驱动程序将插入 fence 写命令的上下文命令流无需通过内核模型直接。 按其内核监视 fence 进度的机制各不相同，具体取决于特定的 GPU 引擎是否支持在受监视的界定的基本或高级实现。

当命令缓冲区在 GPU 上的执行完成后时，图形内核会使用此过程可以发送信号等待挂起的隔离对象的列表，用来阅读其当前的围栏值，并确定是否需要任何等待者已取消等待。

## <a name="span-idgpuwaitspanspan-idgpuwaitspanspan-idgpuwaitspan-gpu-wait"></a><span id="_GPU_wait"></span><span id="_gpu_wait"></span><span id="_GPU_WAIT"></span> GPU 等待


要等待的 GPU 引擎上监视隔离用户模式驱动程序将首先需要刷新其挂起的命令缓冲区然后调用[ *WaitForSynchronizationObjectFromGpuCb* ](https://msdn.microsoft.com/library/windows/hardware/dn906367)指定 fence 对象 （**hSyncObject**) 以及正在等待围栏值。 图形内核将排队到其内部数据库的依赖关系，然后立即返回给用户模式驱动程序，以便它可能仍会等待操作背后的队列起作用。 此命令之后等待操作将未安排执行等待操作已得到满足之前提交的缓冲区。

## <a name="span-idcpusignalspanspan-idcpusignalspanspan-idcpusignalspancpu-signal"></a><span id="CPU_signal"></span><span id="cpu_signal"></span><span id="CPU_SIGNAL"></span>CPU 信号


一个新[ *SignalSynchronizationObjectFromCpuCb* ](https://msdn.microsoft.com/library/windows/hardware/dn906360)已添加了允许的 CPU 监视的 fence 对象发出信号。 时监视的 fence 对象发出信号的 CPU，图形内核将 fence 内存位置使用更新已发出信号值使其成为对任何用户模式下读取器，以及立即取消等待立即可见任何满足等待者。

## <a name="span-idcpuwaitspanspan-idcpuwaitspanspan-idcpuwaitspancpu-wait"></a><span id="CPU_wait"></span><span id="cpu_wait"></span><span id="CPU_WAIT"></span>CPU 等待


一个新[ *WaitForSynchronizationObjectFromCpuCb* ](https://msdn.microsoft.com/library/windows/hardware/dn906366)添加了以允许要等待监视的 fence 对象上的 CPU。 提供两种形式的等待操作。 在第一种形式， *WaitForSynchronizationObjectFromCpuCb*回调被阻止，直至满足等待。 在第二个窗体*WaitForSynchronizationObjectFromCpuCb*使用句柄发出信号后等待条件得到满足的 CPU 事件。

 

 





