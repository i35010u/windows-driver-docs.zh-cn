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
ms.openlocfilehash: fa026692d15c9f50be0fc14929a4298326781444
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544913"
---
# <a name="imxf-interfaces"></a>IMXF 接口


## <span id="imxf_interfaces"></span><span id="IMXF_INTERFACES"></span>


使用同一界面执行 DirectMusic 端口和微型端口驱动程序中的所有 MIDI 传输：[IMXF](https://msdn.microsoft.com/library/windows/hardware/ff536782).

**IMXF**是 DirectMusic MIDI 转换筛选器的 COM 接口。 微型端口驱动程序、 sequencer 和端口驱动程序中处理 MIDI 数据使用的其他实体**IMXF**作为其公共的 COM 接口。 当微型端口驱动程序实现此接口时，它可以参与 MIDI 传输。 [IPortDMus](https://msdn.microsoft.com/library/windows/hardware/ff536879)，后者位于 PortCls，管理**IMXF**。 从捕获设备捕获接收器接口也是**IMXF**接口。

MIDI 数据用户模式和打包加盖时间戳数据的缓冲区中的内核模式之间进行传输。 内核端口驱动程序将这些缓冲区分成单个事件 (请参阅[ **DMU\_内核\_事件**](https://msdn.microsoft.com/library/windows/hardware/ff536340))。 触发时间发生时，高分辨率的 MIDI sequencer 将这些事件传递给微型端口驱动程序。

在输入端内核端口驱动程序从微型端口驱动程序中提取单个输入的消息并生成已打包的缓冲区传递到用户模式。 相应地，DirectMusic 微型端口驱动程序的数据传输模型组成[ **IMXF::PutMessage** ](https://msdn.microsoft.com/library/windows/hardware/ff536791)并[ **IAllocatorMXF::GetMessage** ](https://msdn.microsoft.com/library/windows/hardware/ff536494).

**IMXF**接口支持以下方法：

[**IMXF::ConnectOutput**](https://msdn.microsoft.com/library/windows/hardware/ff536785)

[**IMXF::DisconnectOutput**](https://msdn.microsoft.com/library/windows/hardware/ff536787)

[**IMXF::PutMessage**](https://msdn.microsoft.com/library/windows/hardware/ff536791)

[**IMXF::SetState**](https://msdn.microsoft.com/library/windows/hardware/ff536792)

[IAllocatorMXF](https://msdn.microsoft.com/library/windows/hardware/ff536491)接口扩展**IMXF**通过添加以下方法：

[**IAllocatorMXF::GetMessage**](https://msdn.microsoft.com/library/windows/hardware/ff536494)

[**IAllocatorMXF::GetBufferSize**](https://msdn.microsoft.com/library/windows/hardware/ff536493)

[**IAllocatorMXF::GetBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff536492)

[**IAllocatorMXF::PutBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff536495)

有关使用这些接口的详细信息，请参阅[分配器](allocator.md)。

 

 




