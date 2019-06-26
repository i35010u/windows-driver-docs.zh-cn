---
title: WavePci 端口驱动程序
description: WavePci 端口驱动程序
ms.assetid: 3b4a89d0-f07a-40e1-8c67-62d9cfd96ddd
keywords:
- WavePci 端口驱动程序 WDK 音频
- PortCls WDK 音频，端口驱动程序
- 音频的微型端口驱动程序 WDK，端口驱动程序
- 微型端口驱动程序 WDK 音频，端口驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 25dd17f1cfa3cde254a6908f9c1a2fe8bc5e6cb6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354108"
---
# <a name="wavepci-port-driver"></a>WavePci 端口驱动程序


## <span id="wavepci_port_driver"></span><span id="WAVEPCI_PORT_DRIVER"></span>


**重要**  不再建议使用 WavePci，而是改用 WaverRT。

 

端口驱动程序的可执行的音频设备管理的播放或录制的批流 WavePci 散播-聚集 DMA 传输到或从物理内存中的任何位置。 散播-聚集 DMA，设备可处理的一系列映射组成的缓冲区中的音频数据。 每个映射的物理上连续内存块，但连续映射不一定是连续的彼此。 WavePci 兼容设备是音频适配器上的硬件函数。 通常情况下，适配器是母板上的集成芯片组的一部分，或插入母板上的 PCI 插槽到音频卡上装载。 适配器驱动程序提供了相应[WavePci 微型端口驱动程序](wavepci-miniport-driver.md)绑定到窗体的 WavePci 端口驱动程序对象[批筛选器](wave-filters.md)，可以捕获或呈现批流。

WavePci 端口驱动程序公开[IPortWavePci](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff536905(v=vs.85))微型端口驱动程序的接口。 IPortWavePci 继承基接口中的方法[IPort](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iport)。 此外，IPortWavePci 提供了以下方法：

[**IPortWavePci::NewMasterDmaChannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iportwavepci-newmasterdmachannel)

创建新的主 DMA 通道对象。
[**IPortWavePci::Notify**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iportwavepci-notify)

通知 DMA 控制器具有高级到音频流中的新位置的端口驱动程序。
WavePci 端口驱动程序还公开[IPortWavePciStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iportwavepcistream)微型端口驱动程序的流对象的每个接口。 IPortWavePciStream 继承基接口中的方法[ **IUnknown**](https://docs.microsoft.com/windows/desktop/api/unknwn/nn-unknwn-iunknown)。 IPortWavePciStream 提供了以下其他方法：

[**IPortWavePciStream::GetMapping**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iportwavepcistream-getmapping)

获取从端口驱动程序下一步的映射。
[**IPortWavePciStream::ReleaseMapping**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iportwavepcistream-releasemapping)

释放以前通过的映射**GetMapping**调用。
[**IPortWavePciStream::TerminatePacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iportwavepcistream-terminatepacket)

终止的 I/O 数据包，即使它仅填充了部分与捕获数据。
I/O 数据包是包含与特定映射 IRP 相关联的所有映射的音频缓冲区的一部分。

WavePci 端口和微型端口对象相互通信通过其各自[IPortWavePci](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff536905(v=vs.85))并[IMiniportWavePci](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportwavepci)接口。 此外，WavePci 端口和微型端口流对象相互通信通过其各自[IPortWavePciStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iportwavepcistream)并[IMiniportWavePciStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportwavepcistream)接口。

 

 




