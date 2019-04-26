---
title: WaveCyclic 端口驱动程序
description: WaveCyclic 端口驱动程序
ms.assetid: c5572ae3-0d91-43a6-a49c-c6c005263f5b
keywords:
- WaveCyclic 端口驱动程序 WDK 音频
- PortCls WDK 音频，端口驱动程序
- 音频的微型端口驱动程序 WDK，端口驱动程序
- 微型端口驱动程序 WDK 音频，端口驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 104c1fe39ddc9c4d0b444d58845b55232342c88b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328492"
---
# <a name="wavecyclic-port-driver"></a>WaveCyclic 端口驱动程序


## <span id="wavecyclic_port_driver"></span><span id="WAVECYCLIC_PORT_DRIVER"></span>


**重要**  不再建议使用 WaveCyclic，而是改用 WaverRT。

 

WaveCyclic 端口驱动程序处理循环缓冲区中的音频数据基于 DMA 的音频设备播放或录制批流的管理。 此设备是音频适配器上的硬件函数。 通常情况下，适配器是母板上的集成芯片组的一部分，或插入母板上的 PCI 或 ISA 插槽到音频卡上装载。 适配器驱动程序提供了相应[WaveCyclic 微型端口驱动程序](wavecyclic-miniport-driver.md)绑定到 WaveCyclic 端口驱动程序对象向窗体的驱动程序对象[批筛选器](wave-filters.md)，可以捕获或呈现批流。

WaveCyclic 端口驱动程序公开[IPortWaveCyclic](https://msdn.microsoft.com/library/windows/hardware/ff536899)微型端口驱动程序的接口。 IPortWaveCyclic 继承基接口中的方法[IPort](https://msdn.microsoft.com/library/windows/hardware/ff536842)。 IPortWaveCyclic 提供了以下其他方法：

[**IPortWaveCyclic::NewMasterDmaChannel**](https://msdn.microsoft.com/library/windows/hardware/ff536900)

使用内置的 DMA 控制器创建音频设备的新主 DMA 通道对象。

[**IPortWaveCyclic::NewSlaveDmaChannel**](https://msdn.microsoft.com/library/windows/hardware/ff536902)

创建新从属 DMA 通道对象没有内置 DMA 控制器音频设备。

[**IPortWaveCyclic::Notify**](https://msdn.microsoft.com/library/windows/hardware/ff536903)

通知 DMA 控制器具有高级到音频流中的新位置的端口驱动程序。

WaveCyclic 端口和微型端口驱动程序对象与彼此通信通过其各自[IPortWaveCyclic](https://msdn.microsoft.com/library/windows/hardware/ff536899)并[IMiniportWaveCyclic](https://msdn.microsoft.com/library/windows/hardware/ff536714)接口。 此外，端口驱动程序与微型端口驱动程序的流对象通过其[IMiniportWaveCyclicStream](https://msdn.microsoft.com/library/windows/hardware/ff536715)接口。

 

 




