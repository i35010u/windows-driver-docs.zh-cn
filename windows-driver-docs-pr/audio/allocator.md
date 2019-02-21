---
title: 分配器
description: 分配器
ms.assetid: 8f263288-2f79-4f1d-b740-d78d40f47b32
keywords:
- MIDI 传输 WDK 音频
- 批接收器 WDK 音频，MIDI 传输
- 合成器 WDK 音频，MIDI 传输
- 分配器 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c707da813e32bf476c7947ad63e82dfe8d67c068
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524052"
---
# <a name="allocator"></a>分配器


## <span id="allocator"></span><span id="ALLOCATOR"></span>


与分配器的接口[IMXF](https://msdn.microsoft.com/library/windows/hardware/ff536782)并[IAllocatorMXF](https://msdn.microsoft.com/library/windows/hardware/ff536491)。 这些接口可以重用[ **DMU\_内核\_事件**](https://msdn.microsoft.com/library/windows/hardware/ff536340)结构，无需分配和释放内存。 [**IMXF::PutMessage** ](https://msdn.microsoft.com/library/windows/hardware/ff536791)给分配器提供一种结构并[ **IAllocatorMXF::GetMessage** ](https://msdn.microsoft.com/library/windows/hardware/ff536494)检索全新清零的 DMU\_内核\_事件以供重复使用的分配器结构。 (分配器会创建与空 DMU\_内核\_事件结构在池中，以便永远不会启动都为空。)以下关系图图 Irp 中所示 (DMU 形式\_EVENTHEADER 结构) 到 unpacker 来自 dmusic.dll。

![说明通过端口和微型端口驱动程序的 irp 的流的关系图](images/dmalloc.png)

Unpacker 调用**IAllocatorMXF::GetMessage**来检索一个空[ **DMU\_内核\_事件**](https://msdn.microsoft.com/library/windows/hardware/ff536340)结构。 Unpacker 检索 DMU\_内核\_事件从 IRP 结构、 填充这些结构 （每个 MIDI 事件一个），并将其传递到排序器 （使用其 MXF 接口）。 Sequencer 对其基于其时间戳重新排序，并当到期，将其传递给微型端口驱动程序通过调用**IMXF::PutMessage**。 微型端口驱动程序中拉取 MIDI 数据超出 DMU\_内核\_事件结构，以便它可以将其译为批数据。 通过使用的 DMU\_内核\_事件结构回与另一个分配器**IMXF::PutMessage**调用。

捕获发生相反的情况。 MIDI 数据可以进来从硬件到微型端口驱动程序和微型端口驱动程序调用**IAllocatorMXF::GetMessage**若要获取空 DMU\_内核\_事件结构。 DMU\_内核\_事件结构是使用时间戳和数据填充，传递到捕获接收器通过**IMXF::PutMessage**。 微型端口驱动程序可以传递每个结构的多条消息，如果它设置 DMU\_KEF\_事件\_在 DMU 中不完整标记\_内核\_事件结构。 Dmu 端口驱动程序中的捕获接收器将此原始数据的流分析和发出 DMU\_内核\_事件结构中包含时间戳 MIDI 消息 （每个结构一个）。

还有可能自身发出到捕获接收器加盖时间戳的消息的微型端口驱动程序。 在这种情况下，该驱动程序不会设置 DMU\_KEF\_事件\_位 DMU 的不完整\_内核\_事件。 捕获接收器将标有时间戳结构传递给 packer，它打包成 Irp 的消息并将它们发送到 dmusic.dll 直接。 仅用于记录 MIDI DirectMusic 捕获。 对于批录制内容，请使用 DirectSound 捕获。

Packer 时提取数据从 DMU\_内核\_事件结构，它将放弃使用的 DMU\_内核\_事件结构使用的分配器**IMXF::PutMessage**。 IRP 缓冲区已满时，它被传递给 dmusic.dll。 打包程序从 dmusic.dll 接收空 Irp，填充它们，并完成它们。 以便它始终都有一个用于填充，多个 Irp 保留低速向下传递。

 

 




