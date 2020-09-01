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
ms.openlocfilehash: f774bc06cdf6feed7f7d6398e48161fb7e5414b2
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89208375"
---
# <a name="allocator"></a>分配器


## <span id="allocator"></span><span id="ALLOCATOR"></span>


与分配器的接口是 [IMXF](/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-imxf) 和 [IAllocatorMXF](/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-iallocatormxf)。 通过这些接口，可以重复使用 [**dmu \_ 内核 \_ 事件**](/windows-hardware/drivers/ddi/dmusicks/ns-dmusicks-_dmus_kernel_event) 结构，而无需分配和释放内存。 [**IMXF：:P utmessage**](/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-imxf-putmessage) 为分配器提供一个结构，而 [**IAllocatorMXF：： GetMessage**](/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-iallocatormxf-getmessage) 从分配器检索一个全新的已清零 \_ 的 dmu 内核 \_ 事件结构以供重用。  (创建分配器时，会在池中包含空的 DMU \_ 内核 \_ 事件结构，使其永远不会出现空。 ) 如以下关系图所示： dmu EVENTHEADER 结构形式的 irp (\_) 从 dmusic.dll 到 unpacker。

![说明通过端口和微型端口驱动程序的 irp 流的示意图](images/dmalloc.png)

Unpacker 调用 **IAllocatorMXF：： GetMessage** 以检索空的 [**dmu \_ 内核 \_ 事件**](/windows-hardware/drivers/ddi/dmusicks/ns-dmusicks-_dmus_kernel_event) 结构。 Unpacker 从 IRP 中检索 DMU \_ 内核 \_ 事件结构，在这些 (结构中填充每个 MIDI 事件) ，然后将它们向下传递到 sequencer (使用 MXF 接口) 。 Sequencer 将根据其时间戳重新排序它们，并在它们到期时通过调用 **IMXF：:P utmessage**将它们传递给微型端口驱动程序。 微型端口驱动程序可将 MIDI 数据从 DMU 内核事件结构中提取出来， \_ \_ 使其能够将其呈现到波形数据中。 它将使用的 DMU \_ 内核 \_ 事件结构传递回分配器，并将另一个 **IMXF：:P utmessage** 调用。

反之发生了捕获。 MIDI 数据来自硬件到微型端口驱动程序，微型端口驱动程序调用 **IAllocatorMXF：： GetMessage** 以获取空的 dmu \_ 内核 \_ 事件结构。 DMU \_ 内核 \_ 事件结构填充了时间戳和数据，并通过 **IMXF：:P utmessage**传递到捕获接收器。 如果在 \_ \_ \_ dmu \_ 内核事件结构中设置 dmu KEF 事件不完整标志，微型端口驱动程序可以为每个结构传递多条消息 \_ 。 Dmu 端口驱动程序中的捕获接收器分析此原始数据流，并发出 DMU \_ 内核 \_ 事件结构，其中包含每个结构) 的带时间戳的 MIDI 消息 (。

小型小型驱动程序本身也可以向捕获接收器发出带有时间戳的消息。 在这种情况下，驱动程序不会 \_ \_ \_ 在 dmu 内核事件中设置 dmu KEF 事件未完成位 \_ \_ 。 捕获接收器将带时间戳的结构直接传递到 packer，后者将消息打包到 Irp，并将其发送到 dmusic.dll。 DirectMusic capture 仅用于记录 MIDI。 对于波形录音，请使用 DirectSound 捕获。

当 packer 从 DMU \_ 内核事件结构中提取数据时 \_ ，它会将使用的 dmu \_ 内核 \_ 事件结构丢弃到使用 **IMXF：:P utmessage**的分配器中。 当 IRP 缓冲区已满时，它将向上传递到 dmusic.dll。 Packer 从 dmusic.dll 接收空 Irp，并填充它们并完成。 更多的 Irp 会使进入，以便它始终有一个填充。

 

