---
title: 分配器
description: 分配器
ms.assetid: 8f263288-2f79-4f1d-b740-d78d40f47b32
keywords:
- MIDI 传输 WDK 音频
- 波形接收器音频，MIDI 传输
- 合成 WDK 音频，MIDI 传输
- 分配器 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9536af14fea3622e2852197ed6391ab53c9b8800
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831584"
---
# <a name="allocator"></a>分配器


## <span id="allocator"></span><span id="ALLOCATOR"></span>


与分配器的接口是[IMXF](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-imxf)和[IAllocatorMXF](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-iallocatormxf)。 通过这些接口，可以重复使用[**dmu\_内核\_事件**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/ns-dmusicks-_dmus_kernel_event)结构，而无需分配和释放内存。 [**IMXF：:P utmessage**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-imxf-putmessage)为分配器提供一个结构，而[**IAllocatorMXF：： GetMessage**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-iallocatormxf-getmessage)从分配器检索一个全新的已清零的 DMU\_内核\_事件结构以供重用。 （分配器创建时，会在池中包含空的 DMU\_内核\_事件结构，使其不会启动空。）如下图中所示，Irp （格式为 DMU\_EVENTHEADER 结构）来自 dmusic unpacker。

![说明通过端口和微型端口驱动程序的 irp 流的示意图](images/dmalloc.png)

Unpacker 调用**IAllocatorMXF：： GetMessage**以检索空[**dmu\_内核\_事件**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/ns-dmusicks-_dmus_kernel_event)结构。 Unpacker 从 IRP 检索 DMU\_内核\_事件结构，填充这些结构（每个 MIDI 事件一个），并将它们向下传递到 sequencer （使用其 MXF 接口）。 Sequencer 将根据其时间戳重新排序它们，并在它们到期时通过调用**IMXF：:P utmessage**将它们传递给微型端口驱动程序。 微型端口驱动程序会将 MIDI 数据从 DMU\_内核\_事件结构中取出，使其能够将其呈现到波形数据中。 它将使用的 DMU\_内核\_事件结构传递回分配器，并使用另一个**IMXF：:P utmessage**调用。

反之发生了捕获。 MIDI 数据来自硬件到微型端口驱动程序，微型端口驱动程序调用**IAllocatorMXF：： GetMessage**以获取空的 DMU\_内核\_事件结构。 DMU\_内核\_事件结构填充了时间戳和数据，并通过**IMXF：:P utmessage**传递到捕获接收器。 如果在 DMU\_内核\_事件结构中设置 DMU\_KEF\_事件\_不完整标志，则微型端口驱动程序可以为每个结构传递多条消息。 Dmu 端口驱动程序中的捕获接收器分析此原始数据流，并发出 DMU\_\_内核，其中包含带时间戳的 MIDI 消息（每个结构一个）。

小型小型驱动程序本身也可以向捕获接收器发出带有时间戳的消息。 在这种情况下，驱动程序不会将 DMU\_KEF\_事件\_DMU\_内核\_事件中的未完成位。 捕获接收器将带时间戳的结构直接传递到 packer，后者将消息打包到 Irp，并将其发送到 dmusic。 DirectMusic capture 仅用于记录 MIDI。 对于波形录音，请使用 DirectSound 捕获。

当 packer 从 DMU\_内核\_事件结构中提取数据时，它会将使用的 DMU\_内核\_事件结构丢弃到使用**IMXF：:P utmessage**的分配器中。 当 IRP 缓冲区已满时，它将向上传递到 dmusic。 Packer 从 dmusic 接收空 Irp，并填充它们并完成。 更多的 Irp 会使进入，以便它始终有一个填充。

 

 




