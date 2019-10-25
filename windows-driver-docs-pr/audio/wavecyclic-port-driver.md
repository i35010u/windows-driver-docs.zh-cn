---
title: WaveCyclic 端口驱动程序
description: WaveCyclic 端口驱动程序
ms.assetid: c5572ae3-0d91-43a6-a49c-c6c005263f5b
keywords:
- WaveCyclic 端口驱动程序 WDK 音频
- PortCls WDK 音频，端口驱动程序
- 音频微型端口驱动程序 WDK，端口驱动程序
- 微型端口驱动程序 WDK 音频、端口驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 53c27896c4b149d04a2f3be702b656e3d48c6206
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834000"
---
# <a name="wavecyclic-port-driver"></a>WaveCyclic 端口驱动程序


## <span id="wavecyclic_port_driver"></span><span id="WAVECYCLIC_PORT_DRIVER"></span>


**重要**  不再建议使用 WaveCyclic，改用 WaverRT。

 

WaveCyclic 端口驱动程序通过基于 DMA 的音频设备来管理波形流的播放或录制，该音频设备处理循环缓冲区中的音频数据。 此设备是音频适配器上的硬件功能。 通常，适配器是主板上的集成芯片组的一部分，或者安装在插入到主板上 PCI 或 ISA 插槽的音频卡上。 适配器驱动程序提供了相应的[WaveCyclic 微型端口驱动](wavecyclic-miniport-driver.md)程序对象，该对象绑定到 WaveCyclic 端口驱动程序对象，以形成可捕获或呈现波形流的[波形筛选器](wave-filters.md)。

WaveCyclic 端口驱动程序向微型端口驱动程序公开[IPortWaveCyclic](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iportwavecyclic)接口。 IPortWaveCyclic 继承基接口[IPort](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iport)中的方法。 IPortWaveCyclic 提供了以下附加方法：

[**IPortWaveCyclic::NewMasterDmaChannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iportwavecyclic-newmasterdmachannel)

使用内置 DMA 控制器为音频设备创建一个新的主 DMA 通道对象。

[**IPortWaveCyclic::NewSlaveDmaChannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iportwavecyclic-newslavedmachannel)

为没有内置 DMA 控制器的音频设备创建一个新的从属 DMA 通道对象。

[**IPortWaveCyclic：： Notify**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iportwavecyclic-notify)

通知端口驱动程序 DMA 控制器已前进到音频流中的新位置。

WaveCyclic 端口和微型端口驱动程序对象通过其各自的[IPortWaveCyclic](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iportwavecyclic)和[IMiniportWaveCyclic](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavecyclic)接口相互通信。 此外，端口驱动程序通过其[IMiniportWaveCyclicStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavecyclicstream)接口与微型端口驱动程序的流对象通信。

 

 




