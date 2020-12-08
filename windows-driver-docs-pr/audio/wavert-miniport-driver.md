---
title: WaveRT 微型端口驱动程序
description: WaveRT 微型端口驱动程序
ms.date: 10/01/2020
ms.localizationpriority: medium
ms.openlocfilehash: a9a5e05e7c5c9043fdcac3fe8f9cd82dd4b0d540
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798779"
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

[IMiniportWaveRTStream](/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavertstream)接口继承 [**IUnknown**](/windows/win32/api/unknwn/nn-unknwn-iunknown)接口中的方法。 IMiniportWaveRTStream 提供了以下附加方法：

[**IMiniportWaveRTStream：： AllocateAudioBuffer**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavertstream-allocateaudiobuffer) 分配音频数据的循环缓冲区。

[**IMiniportWaveRTStream::FreeAudioBuffer**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavertstream-freeaudiobuffer)

释放以前使用对 [**IMiniportWaveRTStream：： AllocateAudioBuffer**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavertstream-allocateaudiobuffer)的调用分配的音频缓冲区。

[**IMiniportWaveRTStream::GetClockRegister**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavertstream-getclockregister)

检索端口驱动程序必须用于向音频子系统及其客户端公开时钟寄存器的信息。

[**IMiniportWaveRTStream::GetHWLatency**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavertstream-gethwlatency)

检索有关音频硬件中的流延迟源的信息。

[**IMiniportWaveRTStream::GetPosition**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavertstream-getposition)

检索当前的播放位置或记录位置作为缓冲区开头的字节偏移量。

[**IMiniportWaveRTStream::GetPositionRegister**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavertstream-getpositionregister)

检索端口驱动程序必须用于向音频子系统及其客户端公开位置注册的信息。

[**IMiniportWaveRTStream::SetFormat**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavertstream-setformat)

设置波形流的数据格式。

[**IMiniportWaveRTStream：： SetState**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavertstream-setstate)

更改音频流的传输状态。
