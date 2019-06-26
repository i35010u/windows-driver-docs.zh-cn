---
title: IMXF 接口
description: IMXF 接口
ms.assetid: 3782f812-bb95-4735-9635-e721ccda92b5
keywords:
- IMXF
- MIDI 传输 WDK 音频
- 批接收器 WDK 音频，MIDI 传输
- 合成器 WDK 音频，MIDI 传输
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7989fe5ac93cde4b31742e467ab0c63b31cdc64d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359906"
---
# <a name="imxf-interfaces"></a>IMXF 接口


## <span id="imxf_interfaces"></span><span id="IMXF_INTERFACES"></span>


使用同一界面执行 DirectMusic 端口和微型端口驱动程序中的所有 MIDI 传输：[IMXF](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nn-dmusicks-imxf).

**IMXF**是 DirectMusic MIDI 转换筛选器的 COM 接口。 微型端口驱动程序、 sequencer 和端口驱动程序中处理 MIDI 数据使用的其他实体**IMXF**作为其公共的 COM 接口。 当微型端口驱动程序实现此接口时，它可以参与 MIDI 传输。 [IPortDMus](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nn-dmusicks-iportdmus)，后者位于 PortCls，管理**IMXF**。 从捕获设备捕获接收器接口也是**IMXF**接口。

MIDI 数据用户模式和打包加盖时间戳数据的缓冲区中的内核模式之间进行传输。 内核端口驱动程序将这些缓冲区分成单个事件 (请参阅[ **DMU\_内核\_事件**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/ns-dmusicks-_dmus_kernel_event))。 触发时间发生时，高分辨率的 MIDI sequencer 将这些事件传递给微型端口驱动程序。

在输入端内核端口驱动程序从微型端口驱动程序中提取单个输入的消息并生成已打包的缓冲区传递到用户模式。 相应地，DirectMusic 微型端口驱动程序的数据传输模型组成[ **IMXF::PutMessage** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nf-dmusicks-imxf-putmessage)并[ **IAllocatorMXF::GetMessage** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nf-dmusicks-iallocatormxf-getmessage).

**IMXF**接口支持以下方法：

[**IMXF::ConnectOutput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nf-dmusicks-imxf-connectoutput)

[**IMXF::DisconnectOutput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nf-dmusicks-imxf-disconnectoutput)

[**IMXF::PutMessage**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nf-dmusicks-imxf-putmessage)

[**IMXF::SetState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nf-dmusicks-imxf-setstate)

[IAllocatorMXF](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nn-dmusicks-iallocatormxf)接口扩展**IMXF**通过添加以下方法：

[**IAllocatorMXF::GetMessage**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nf-dmusicks-iallocatormxf-getmessage)

[**IAllocatorMXF::GetBufferSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nf-dmusicks-iallocatormxf-getbuffersize)

[**IAllocatorMXF::GetBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nf-dmusicks-iallocatormxf-getbuffer)

[**IAllocatorMXF::PutBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nf-dmusicks-iallocatormxf-putbuffer)

有关使用这些接口的详细信息，请参阅[分配器](allocator.md)。

 

 




