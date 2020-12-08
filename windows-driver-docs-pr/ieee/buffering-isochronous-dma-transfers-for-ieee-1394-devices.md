---
title: 缓冲 IEEE 1394 设备的常时等量 DMA 传输
description: 缓冲 IEEE 1394 设备的常时等量 DMA 传输
keywords:
- 同步 i/o WDK IEEE 1394 总线，缓冲 DMA 传输
- 缓冲 WDK IEEE 1394 总线
- DMA 传输 WDK IEEE 1394 总线
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 85edca3f7ed4503db4f390dc66b7c2160d248ba7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824149"
---
# <a name="buffering-isochronous-dma-transfers-for-ieee-1394-devices"></a>缓冲 IEEE 1394 设备的常时等量 DMA 传输





一旦开始，同步传输将一直持续到暂停。 主机控制器必须具有可用的缓冲区来处理事务的需求。 总线驱动程序使用附加到资源句柄的缓冲区，直到它们用完，然后停止 DMA。 在此之前，驱动程序会附加更多的缓冲区来继续事务。 缓冲区的 ISOCH \_ 描述符可以选择在总线驱动程序完成缓冲区时提供回调，驱动程序可以使用它附加更多缓冲区。 为了获得最佳性能，驱动程序应一次附加多个缓冲区，并只为最后一个缓冲区提供回调，以指示缓冲区的提供已用完。

下图说明了在同步传输中使用的缓冲区。

![说明同步传输中使用的缓冲区的关系图](images/1394lin.png)

 

 




