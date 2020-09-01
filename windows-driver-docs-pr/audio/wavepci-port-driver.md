---
title: WavePci 端口驱动程序
description: WavePci 端口驱动程序
ms.assetid: 3b4a89d0-f07a-40e1-8c67-62d9cfd96ddd
keywords:
- WavePci 端口驱动程序 WDK 音频
- PortCls WDK 音频，端口驱动程序
- 音频微型端口驱动程序 WDK，端口驱动程序
- 微型端口驱动程序 WDK 音频、端口驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5351fa208570e7a9e43ac4c2cf28dfebd8b25d93
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89210267"
---
# <a name="wavepci-port-driver"></a>WavePci 端口驱动程序


## <span id="wavepci_port_driver"></span><span id="WAVEPCI_PORT_DRIVER"></span>


**重要提示**   不再建议使用 WavePci，而是改用 WaverRT。

 

WavePci 端口驱动程序可通过音频设备管理波形流的播放或录制，该设备可执行与物理内存中的任何位置之间的散播/聚集 DMA 传输。 使用散播/聚集 DMA，设备可以处理由一系列映射组成的缓冲区中的音频数据。 每个映射都是物理上连续内存的块，但后续映射不一定彼此相邻。 WavePci 兼容设备是音频适配器上的硬件功能。 通常，适配器是主板上的集成芯片组的一部分，或者安装在插入到主板 PCI 插槽的音频卡上。 适配器驱动程序提供了相应的 [WavePci 微型端口驱动程序，该驱动程序](wavepci-miniport-driver.md) 绑定到 WavePci 端口驱动程序对象，以形成可捕获或呈现波形流的 [波形筛选器](wave-filters.md) 。

WavePci 端口驱动程序向微型端口驱动程序公开 [IPortWavePci](/previous-versions/windows/hardware/drivers/ff536905(v=vs.85)) 接口。 IPortWavePci 继承基接口 [IPort](/windows-hardware/drivers/ddi/portcls/nn-portcls-iport)中的方法。 此外，IPortWavePci 提供了以下方法：

[**IPortWavePci::NewMasterDmaChannel**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iportwavepci-newmasterdmachannel)

创建新的主 DMA 通道对象。
[**IPortWavePci：： Notify**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iportwavepci-notify)

通知端口驱动程序 DMA 控制器已前进到音频流中的新位置。
WavePci 端口驱动程序还向每个微型端口驱动程序的流对象公开 [IPortWavePciStream](/windows-hardware/drivers/ddi/portcls/nn-portcls-iportwavepcistream) 接口。 IPortWavePciStream 继承基接口 [**IUnknown**](/windows/desktop/api/unknwn/nn-unknwn-iunknown)中的方法。 IPortWavePciStream 提供了以下附加方法：

[**IPortWavePciStream::GetMapping**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iportwavepcistream-getmapping)

获取端口驱动程序的下一个映射。
[**IPortWavePciStream::ReleaseMapping**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iportwavepcistream-releasemapping)

释放先前由 **GetMapping** 调用获得的映射。
[**IPortWavePciStream::TerminatePacket**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iportwavepcistream-terminatepacket)

终止 i/o 数据包，即使它仅部分填充了捕获数据。
I/o 数据包是音频缓冲区的一部分，其中包含与特定映射 IRP 关联的所有映射。

WavePci 端口和微型端口对象通过各自的 [IPortWavePci](/previous-versions/windows/hardware/drivers/ff536905(v=vs.85)) 和 [IMiniportWavePci](/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavepci) 接口相互通信。 此外，WavePci 端口和微型端口流对象通过其各自的 [IPortWavePciStream](/windows-hardware/drivers/ddi/portcls/nn-portcls-iportwavepcistream) 和 [IMiniportWavePciStream](/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavepcistream) 接口相互通信。

 

