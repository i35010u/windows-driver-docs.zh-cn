---
title: WaveRT 微型端口驱动程序
description: WaveRT 微型端口驱动程序
ms.assetid: 154dc921-424f-4021-8f17-5482ceef99a8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f91f04e5f652e62d7cc0ed59cedefe09bae7256c
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90716620"
---
# <a name="wavert-miniport-driver"></a>WaveRT 微型端口驱动程序


WaveRT 微型端口驱动程序在 Windows Vista 和更高版本的 Windows 操作系统中受支持，它管理波形渲染或波形捕获音频设备的硬件相关功能。 WaveRT 友好音频设备具有散播/聚集 DMA 硬件，可以在物理内存中的任何位置传输音频数据。

WaveRT 微型端口驱动程序必须实现两个接口：

-   [IMiniportWaveRT](/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavert)。 此接口执行微型端口驱动程序初始化、通道枚举和流创建。

-   [IMiniportWaveRTStream](/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavertstream)。 此接口管理波形流并公开微型端口驱动程序的大部分功能。

有关如何设计补充 WaveRT 端口驱动程序的 WaveRT 微型端口驱动程序的信息，请参阅 [开发 WaveRT 微型端口驱动程序](developing-a-wavert-miniport-driver.md) 主题。

### <a name="span-idiminiportwavertspanspan-idiminiportwavertspaniminiportwavert"></a><span id="iminiportwavert"></span><span id="IMINIPORTWAVERT"></span>IMiniportWaveRT

[IMiniportWaveRT](/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavert)接口提供了以下方法：

[**IMiniportWaveRT：： Init**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavert-init)

初始化微型端口对象。

[**IMiniportWaveRT：： Newstream.ischecked**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavert-newstream)

创建新的流对象。

[**IMiniportWaveRT::GetDeviceDescription**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavert-getdevicedescription)

返回一个指针，该指针指向描述设备的 [**设备 \_ 说明**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_description) 结构。

### <a name="span-idiminiportwavertstreamspanspan-idiminiportwavertstreamspaniminiportwavertstream"></a><span id="iminiportwavertstream"></span><span id="IMINIPORTWAVERTSTREAM"></span>IMiniportWaveRTStream

[IMiniportWaveRTStream](/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavertstream)接口继承[**IUnknown**](/windows/win32/api/unknwn/nn-unknwn-iunknown)接口中的方法。 IMiniportWaveRTStream 提供了以下附加方法：

[**IMiniportWaveRTStream::AllocateAudioBuffer**](/previous-versions/windows/hardware/drivers/ff536744(v=vs.85))

分配音频数据的循环缓冲区。

[**IMiniportWaveRTStream::FreeAudioBuffer**](/previous-versions/windows/hardware/drivers/ff536745(v=vs.85))

释放以前使用对 [**IMiniportWaveRTStream：： AllocateAudioBuffer**](/previous-versions/windows/hardware/drivers/ff536744(v=vs.85))的调用分配的音频缓冲区。

[**IMiniportWaveRTStream::GetClockRegister**](/previous-versions/windows/hardware/drivers/ff536746(v=vs.85))

检索端口驱动程序必须用于向音频子系统及其客户端公开时钟寄存器的信息。

[**IMiniportWaveRTStream::GetHWLatency**](/previous-versions/windows/hardware/drivers/ff536747(v=vs.85))

检索有关音频硬件中的流延迟源的信息。

[**IMiniportWaveRTStream::GetPosition**](/previous-versions/windows/hardware/drivers/ff536749(v=vs.85))

检索当前的播放位置或记录位置作为缓冲区开头的字节偏移量。

[**IMiniportWaveRTStream::GetPositionRegister**](/previous-versions/windows/hardware/drivers/ff536752(v=vs.85))

检索端口驱动程序必须用于向音频子系统及其客户端公开位置注册的信息。

[**IMiniportWaveRTStream::SetFormat**](/previous-versions/windows/hardware/drivers/ff536753(v=vs.85))

设置波形流的数据格式。

[**IMiniportWaveRTStream：： SetState**](/previous-versions/windows/hardware/drivers/ff536756(v=vs.85))

更改音频流的传输状态。

 

