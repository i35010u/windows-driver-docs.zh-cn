---
title: 流指针和 IRP 取消
description: 流指针和 IRP 取消
ms.assetid: ce392496-ca07-497d-af8a-709239a7bd5e
keywords:
- 流指针 WDK AVStream，IRP 取消
- IRP 取消 WDK AVStream
- 正在取消 Irp WDK AVStream
- 锁定的流指针 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 784f1ea2f73f89062a22cf82586b00854d8e7d72
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377793"
---
# <a name="stream-pointers-and-irp-cancellation"></a>流指针和 IRP 取消





如果帧已对其进行引用的锁定的流指针，不能取消 IRP 对应于此帧。 请参阅[锁定和解锁 Stream 指针](locking-and-unlocking-stream-pointers.md)。

下表列出了你微型驱动程序可用于支持 IRP 取消操作的技术。 取消策略应基于您微型驱动程序的流访问要求，最左侧列中所述。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>如果你需要...</th>
<th>执行此操作</th>
<th>备注</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Brief 对在单一访问点的流数据的访问</p></td>
<td><p>调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-kspingetleadingedgestreampointer" data-raw-source="[&lt;strong&gt;KsPinGetLeadingEdgeStreamPointer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-kspingetleadingedgestreampointer)"> <strong>KsPinGetLeadingEdgeStreamPointer</strong> </a>与<em>状态</em>参数设置为 KSSTREAM_POINTER_STATE_LOCKED。 然后调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointerunlock" data-raw-source="[&lt;strong&gt;KsStreamPointerUnlock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointerunlock)"> <strong>KsStreamPointerUnlock</strong> </a>或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointeradvanceoffsetsandunlock" data-raw-source="[&lt;strong&gt;KsStreamPointerAdvanceOffsetsAndUnlock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointeradvanceoffsetsandunlock)"> <strong>KsStreamPointerAdvanceOffsetsAndUnlock</strong> </a>立即处理后完成。</p></td>
<td><p>提供对取消的快速响应能力，除非该线程阻塞之间获取指针和对其解除锁定。</p></td>
</tr>
<tr class="even">
<td><p>无限期时间长度的访问权限，但可以放弃取消回调的上下文中的声明</p></td>
<td><p>调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointerclone" data-raw-source="[&lt;strong&gt;KsStreamPointerClone&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointerclone)"> <strong>KsStreamPointerClone</strong> </a>若要克隆的锁定的流指针 （通常前导边缘），解锁，并响应<em>CancelCallback</em>。 使用队列的数值调节钮持有锁，因此在 DISPATCH_LEVEL 时出现回调。 相应地，供应商提供<em>CancelCallback</em>例程无法执行获取互斥体的队列操作或调用函数。 相反，在回调例程中，微型驱动程序验证关联的数据将更高版本，访问，然后调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointerdelete" data-raw-source="[&lt;strong&gt;KsStreamPointerDelete&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointerdelete)"> <strong>KsStreamPointerDelete</strong></a>。</p></td>
<td><p>可以会更难实现，但通常会提供高效的访问和快速响应取消操作之间的最佳平衡。</p></td>
</tr>
<tr class="odd">
<td><p>定期访问到框架，并且可以容忍访问之间帧的亮点</p></td>
<td><p>维护解锁的克隆并调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointerlock" data-raw-source="[&lt;strong&gt;KsStreamPointerLock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointerlock)"> <strong>KsStreamPointerLock</strong> </a>在访问时锁定。 如果取消帧下, 一步尝试锁定流指针失败，并可以调用微型驱动程序<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointerdelete" data-raw-source="[&lt;strong&gt;KsStreamPointerDelete&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointerdelete)"> <strong>KsStreamPointerDelete</strong></a>。</p></td>
<td><p>正如第一个选项，取消操作的响应能力是锁定的时间流指针的函数。</p></td>
</tr>
<tr class="even">
<td><p>无限期访问时间长度并不能取消回调的响应中的声明</p></td>
<td><p>维护任意长度的时间，以防止取消锁定的克隆流指针。 若要创建的克隆流指针，调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointerclone" data-raw-source="[&lt;strong&gt;KsStreamPointerClone&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointerclone)"> <strong>KsStreamPointerClone</strong></a>。 然后调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointerlock" data-raw-source="[&lt;strong&gt;KsStreamPointerLock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointerlock)"> <strong>KsStreamPointerLock</strong> </a>并<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointerunlock" data-raw-source="[&lt;strong&gt;KsStreamPointerUnlock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointerunlock)"> <strong>KsStreamPointerUnlock</strong> </a>锁定或解锁克隆。</p></td>
<td><p>取消操作的响应能力可能会很差。 请考虑使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointerscheduletimeout" data-raw-source="[&lt;strong&gt;stream pointer timeouts&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointerscheduletimeout)"><strong>流指针超时</strong></a>利用这种技术。</p></td>
</tr>
</tbody>
</table>

 

如果帧已对其进行引用的流指针，微型驱动程序可以调用[ **KsStreamPointerGetIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointergetirp)访问 IRP 对应于此帧。 若要检索与帧相关联的内存描述符列表 (MDL)，请调用[ **KsStreamPointerGetMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointergetmdl)。

 

 




