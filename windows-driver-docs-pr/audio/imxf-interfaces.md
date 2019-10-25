---
title: IMXF 接口
description: IMXF 接口
ms.assetid: 3782f812-bb95-4735-9635-e721ccda92b5
keywords:
- IMXF
- MIDI 传输 WDK 音频
- 波形接收器音频，MIDI 传输
- 合成 WDK 音频，MIDI 传输
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2baafb72144c9d32c858ca4cf8f420506a72bb91
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833228"
---
# <a name="imxf-interfaces"></a>IMXF 接口


## <span id="imxf_interfaces"></span><span id="IMXF_INTERFACES"></span>


使用同一个接口执行 DirectMusic 端口和微型端口驱动程序中的所有 MIDI 传输： [IMXF](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-imxf)。

**IMXF**是用于 DirectMusic MIDI 转换筛选器的 COM 接口。 端口驱动程序中用于处理 MIDI 数据的微型端口驱动程序、sequencer 和其他实体使用**IMXF**作为其公共 COM 接口。 当微型端口驱动程序实现此接口时，它可以参与 MIDI 传输。 [IPortDMus](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-iportdmus)位于 PortCls 中，用于管理**IMXF**。 捕获设备到捕获接收器的接口也是**IMXF**接口。

MIDI 数据在用户模式和内核模式之间传输到压缩的带时间戳的数据的缓冲区中。 内核端口驱动程序将这些缓冲区分解为单独的事件（请参阅[**dmu\_内核\_事件**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/ns-dmusicks-_dmus_kernel_event)）。 当触发时间发生时，高分辨率 MIDI sequencer 将这些事件传递给微型端口驱动程序。

在输入端，内核端口驱动程序从微型端口驱动程序中提取各个输入消息，并生成打包的缓冲区以传递到用户模式。 相应地，DirectMusic 微型端口驱动程序的数据传输模型包含[**IMXF：:P utmessage**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-imxf-putmessage)和[**IAllocatorMXF：： GetMessage**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-iallocatormxf-getmessage)。

**IMXF**接口支持以下方法：

[**IMXF::ConnectOutput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-imxf-connectoutput)

[**IMXF：:D isconnectOutput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-imxf-disconnectoutput)

[**IMXF：:P utMessage**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-imxf-putmessage)

[**IMXF：： SetState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-imxf-setstate)

[IAllocatorMXF](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-iallocatormxf)接口通过添加以下方法来扩展**IMXF** ：

[**IAllocatorMXF：： GetMessage**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-iallocatormxf-getmessage)

[**IAllocatorMXF::GetBufferSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-iallocatormxf-getbuffersize)

[**IAllocatorMXF：： GetBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-iallocatormxf-getbuffer)

[**IAllocatorMXF：:P utBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-iallocatormxf-putbuffer)

有关使用这些接口的详细信息，请参阅[分配](allocator.md)器。

 

 




