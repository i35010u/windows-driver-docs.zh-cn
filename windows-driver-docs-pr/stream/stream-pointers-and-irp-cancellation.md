---
title: 流指针和 IRP 取消
description: 流指针和 IRP 取消
ms.assetid: ce392496-ca07-497d-af8a-709239a7bd5e
keywords:
- 流指针 WDK AVStream，IRP 取消
- IRP 取消 WDK AVStream
- 取消 Irp WDK AVStream
- 锁定的流指针 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 88d269fe9055ad7b8883d9612e0b0540a10960d2
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186265"
---
# <a name="stream-pointers-and-irp-cancellation"></a>流指针和 IRP 取消





如果框架具有引用它的锁定流指针，则不能取消与此帧对应的 IRP。 请参阅 [锁定和解锁流指针](locking-and-unlocking-stream-pointers.md)。

下表列出了微型驱动程序可用于支持 IRP 取消的技术。 你的取消策略应基于微型驱动程序的流访问需求，如最左侧的专栏中所述。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>如果需要，</th>
<th>操作</th>
<th>注释</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>在单个接入点上对流数据进行短暂访问</p></td>
<td><p>调用 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kspingetleadingedgestreampointer" data-raw-source="[&lt;strong&gt;KsPinGetLeadingEdgeStreamPointer&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/nf-ks-kspingetleadingedgestreampointer)"><strong>KsPinGetLeadingEdgeStreamPointer</strong></a> ，并将 <em>状态</em> 参数设置为 KSSTREAM_POINTER_STATE_LOCKED。 完成处理后，立即调用 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerunlock" data-raw-source="[&lt;strong&gt;KsStreamPointerUnlock&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerunlock)"><strong>KsStreamPointerUnlock</strong></a> 或 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointeradvanceoffsetsandunlock" data-raw-source="[&lt;strong&gt;KsStreamPointerAdvanceOffsetsAndUnlock&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointeradvanceoffsetsandunlock)"><strong>KsStreamPointerAdvanceOffsetsAndUnlock</strong></a> 。</p></td>
<td><p>提供对取消的快速响应，除非线程在获取指针和解锁指针之间阻止。</p></td>
</tr>
<tr class="even">
<td><p>无限长的访问时间，但在取消回调的上下文中可以放弃声明</p></td>
<td><p>调用 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerclone" data-raw-source="[&lt;strong&gt;KsStreamPointerClone&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerclone)"><strong>KsStreamPointerClone</strong></a> 可克隆锁定的流指针 (通常为) 的主要边缘，对其进行解锁，并对 <em>CancelCallback</em>作出响应。 回调发生，并保持队列的旋转锁，因此 DISPATCH_LEVEL。 因此，供应商提供的 <em>CancelCallback</em> 例程无法执行队列操作，也无法调用获取互斥体的函数。 相反，在回调例程中，微型驱动程序将验证以后不会访问关联数据，然后调用 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerdelete" data-raw-source="[&lt;strong&gt;KsStreamPointerDelete&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerdelete)"><strong>KsStreamPointerDelete</strong></a>。</p></td>
<td><p>更难实现，但通常会在有效访问和快速响应取消之间提供最佳平衡。</p></td>
</tr>
<tr class="odd">
<td><p>定期访问帧，可以容忍访问之间的帧的消失</p></td>
<td><p>维护未锁定的克隆，并调用 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerlock" data-raw-source="[&lt;strong&gt;KsStreamPointerLock&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerlock)"><strong>KsStreamPointerLock</strong></a> 在访问时将其锁定。 如果已取消帧，则下一次尝试锁定流指针将失败，并且微型驱动程序可以调用 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerdelete" data-raw-source="[&lt;strong&gt;KsStreamPointerDelete&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerdelete)"><strong>KsStreamPointerDelete</strong></a>。</p></td>
<td><p>与第一个选项一样，对取消的响应是流指针锁定时间的一个函数。</p></td>
</tr>
<tr class="even">
<td><p>无限长的访问时间，并且无法在响应回调时放弃声明</p></td>
<td><p>在任意时间段维护锁定的克隆流指针，以防止取消。 若要创建克隆流指针，请调用 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerclone" data-raw-source="[&lt;strong&gt;KsStreamPointerClone&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerclone)"><strong>KsStreamPointerClone</strong></a>。 然后，调用 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerlock" data-raw-source="[&lt;strong&gt;KsStreamPointerLock&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerlock)"><strong>KsStreamPointerLock</strong></a> 和 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerunlock" data-raw-source="[&lt;strong&gt;KsStreamPointerUnlock&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerunlock)"><strong>KsStreamPointerUnlock</strong></a> 将克隆锁定或解锁。</p></td>
<td><p>对取消的响应可能会很差。 请考虑将 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerscheduletimeout" data-raw-source="[&lt;strong&gt;stream pointer timeouts&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerscheduletimeout)"><strong>流指针超时</strong></a> 用于此技术。</p></td>
</tr>
</tbody>
</table>

 

如果帧具有引用它的流指针，则微型驱动程序可以调用 [**KsStreamPointerGetIrp**](/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointergetirp) 来访问与此帧对应的 IRP。 若要检索与帧关联 (MDL) 的内存描述符列表，请调用 [**KsStreamPointerGetMdl**](/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointergetmdl)。

 

