---
title: WaveRT 微型端口驱动程序
description: WaveRT 微型端口驱动程序
ms.assetid: 154dc921-424f-4021-8f17-5482ceef99a8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 064146e8eca9a2ffb80f927bd5856cad0711465d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364785"
---
# <a name="wavert-miniport-driver"></a>WaveRT 微型端口驱动程序


WaveRT 微型端口驱动程序支持在 Windows Vista 和更高版本的 Windows 操作系统和它所管理的批呈现或批捕获音频设备依赖于硬件的函数。 WaveRT 友好音频设备具有可将音频数据的物理内存中的任何位置来回传输的分散/聚拢 DMA 硬件。

WaveRT 微型端口驱动程序必须实现两个接口：

-   [IMiniportWaveRT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportwavert)。 此接口执行的微型端口驱动程序初始化、 通道枚举和流创建。

-   [IMiniportWaveRTStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportwavertstream)。 此接口管理批流，并会公开大部分的微型端口驱动程序的功能。

有关如何设计进行了补充 WaveRT 端口驱动程序的 WaveRT 微型端口驱动程序的信息，请参阅[开发 WaveRT 微型端口驱动程序](developing-a-wavert-miniport-driver.md)主题。

### <a name="span-idiminiportwavertspanspan-idiminiportwavertspaniminiportwavert"></a><span id="iminiportwavert"></span><span id="IMINIPORTWAVERT"></span>IMiniportWaveRT

[IMiniportWaveRT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportwavert)接口提供了以下方法：

[**IMiniportWaveRT::Init**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavert-init)

初始化微型端口对象。

[**IMiniportWaveRT::NewStream**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavert-newstream)

创建新的流对象。

[**IMiniportWaveRT::GetDeviceDescription**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavert-getdevicedescription)

返回一个指向[**设备\_说明**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_description)结构描述设备。

### <a name="span-idiminiportwavertstreamspanspan-idiminiportwavertstreamspaniminiportwavertstream"></a><span id="iminiportwavertstream"></span><span id="IMINIPORTWAVERTSTREAM"></span>IMiniportWaveRTStream

[IMiniportWaveRTStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportwavertstream)接口继承的方法从[ **IUnknown** ](https://docs.microsoft.com/windows/desktop/api/unknwn/nn-unknwn-iunknown)接口。 IMiniportWaveRTStream 提供了以下其他方法：

[**IMiniportWaveRTStream::AllocateAudioBuffer**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff536744(v=vs.85))

音频数据分配一个循环缓冲区。

[**IMiniportWaveRTStream::FreeAudioBuffer**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff536745(v=vs.85))

释放以前通过调用分配的音频缓冲区[ **IMiniportWaveRTStream::AllocateAudioBuffer**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff536744(v=vs.85))。

[**IMiniportWaveRTStream::GetClockRegister**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff536746(v=vs.85))

检索端口驱动程序必须具有要公开的时钟寄存器音频子系统和其客户端的信息。

[**IMiniportWaveRTStream::GetHWLatency**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff536747(v=vs.85))

检索有关流中的延迟时间的音频硬件的源的信息。

[**IMiniportWaveRTStream::GetPosition**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff536749(v=vs.85))

检索当前播放或记录位置的字节偏移量从缓冲区的开头。

[**IMiniportWaveRTStream::GetPositionRegister**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff536752(v=vs.85))

检索端口驱动程序必须具有要公开的音频子系统和其客户端位置注册的信息。

[**IMiniportWaveRTStream::SetFormat**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff536753(v=vs.85))

设置批流的数据格式。

[**IMiniportWaveRTStream::SetState**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff536756(v=vs.85))

更改音频流的传输状态。

 

 




