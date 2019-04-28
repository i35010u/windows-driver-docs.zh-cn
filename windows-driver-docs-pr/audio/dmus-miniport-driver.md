---
title: DMus 微型端口驱动程序
description: DMus 微型端口驱动程序
ms.assetid: a0ce6545-2050-49fb-88b5-a75dcd4c7ebc
keywords:
- 音频的微型端口驱动程序 WDK Dmu
- 微型端口驱动程序 WDK 音频 Dmu
- DirectMusic WDK 音频，微型端口驱动程序
- Dmu 微型端口驱动程序 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c703e8dba133d2b12eb5a54daf5a3d17ec11e25d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333757"
---
# <a name="dmus-miniport-driver"></a>DMus 微型端口驱动程序


## <span id="dmus_miniport_driver"></span><span id="DMUS_MINIPORT_DRIVER"></span>


Dmu 微型端口驱动程序管理的高级 MIDI 设备依赖于硬件的函数。 这些设备支持 DirectMusic 功能，例如精度 sequencer 计时、 可下载的声音 (DL) 和通道组。 Dmu 微型端口驱动程序可以使用设备，例如 MPU 401 实现高性能。 可以通过微型端口驱动程序或端口驱动程序，具体取决于硬件的功能来处理计时。 Dmu 微型端口驱动程序还可以支持软件合成器生成的 wave 输出流。

MIDI 硬件设备的 Dmu 微型端口驱动程序应支持两个接口：

-   微型端口接口初始化微型端口对象，并创建 MIDI 流。

-   流接口管理 MIDI 流，并会公开大部分的微型端口驱动程序的功能。

微型端口接口[IMiniportDMus](https://msdn.microsoft.com/library/windows/hardware/ff536699)，继承中的方法[IMiniport](https://msdn.microsoft.com/library/windows/hardware/ff536698)接口。 **IMiniportDMus**提供了以下其他方法：

[**IMiniportDMus::Init**](https://msdn.microsoft.com/library/windows/hardware/ff536700)

初始化微型端口对象。

[**IMiniportDMus::NewStream**](https://msdn.microsoft.com/library/windows/hardware/ff536701)

创建新的流对象。

[**IMiniportDMus::Service**](https://msdn.microsoft.com/library/windows/hardware/ff536702)

通知服务的请求的微型端口驱动程序。

流接口[IMXF](https://msdn.microsoft.com/library/windows/hardware/ff536782)，继承中的方法**IUnknown**接口。 **IMXF**提供了以下其他方法：

[**IMXF::ConnectOutput**](https://msdn.microsoft.com/library/windows/hardware/ff536785)

连接到为数据源，此流对象**IMXF**的另一个流对象，它是数据接收器的接口。

[**IMXF::DisconnectOutput**](https://msdn.microsoft.com/library/windows/hardware/ff536787)

断开此流对象从**IMXF**另一个是数据接收器的流对象的接口。

[**IMXF::PutMessage**](https://msdn.microsoft.com/library/windows/hardware/ff536791)

Pass [ **DMU\_内核\_事件**](https://msdn.microsoft.com/library/windows/hardware/ff536340)数据接收器的结构。

[**IMXF::SetState**](https://msdn.microsoft.com/library/windows/hardware/ff536792)

设置流的状态。

另外，Dmu 微型端口驱动程序[ISynthSinkDMus](https://msdn.microsoft.com/library/windows/hardware/ff537011)接口提供的软件合成器 DLS 功能。 **ISynthSinkDMus**继承基接口中的方法**IMXF**。 **ISynthSinkDMus**提供了以下其他方法：

[**ISynthSinkDMus::RefTimeToSample**](https://msdn.microsoft.com/library/windows/hardware/ff537013)

将引用时间转换为示例时间。

[**ISynthSinkDMus::Render**](https://msdn.microsoft.com/library/windows/hardware/ff537015)

将批数据呈现到批接收器的缓冲区。

[**ISynthSinkDMus::SampleToRefTime**](https://msdn.microsoft.com/library/windows/hardware/ff537018)

将示例时间转换为引用时间。

[**ISynthSinkDMus::SyncToMaster**](https://msdn.microsoft.com/library/windows/hardware/ff537019)

将同步到 master 时钟示例时钟。

端口驱动程序的批接收器调用**ISynthSinkDMus::Render**读取批 PCM 从其 MIDI 合成器生成的数据输入流。 有关批接收器的详细信息，请参阅[内核模式软件合成器的批接收器](a-wave-sink-for-kernel-mode-software-synthesizers.md)。

微型端口驱动程序 Dmu 端口驱动程序上调用以下接口：

[IPortDMus](https://msdn.microsoft.com/library/windows/hardware/ff536879)

[IAllocatorMXF](https://msdn.microsoft.com/library/windows/hardware/ff536491)

[IMasterClock](https://msdn.microsoft.com/library/windows/hardware/ff536696)

PortCls 包含 UART 函数具有的 MIDI 设备的内置 Dmu 微型端口驱动程序。 有关详细信息，请参阅[ **PcNewMiniport**](https://msdn.microsoft.com/library/windows/hardware/ff537714)。

 

 




