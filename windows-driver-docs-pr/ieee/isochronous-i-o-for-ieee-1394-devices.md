---
title: IEEE 1394 设备的常时等量 I/O
description: IEEE 1394 设备的常时等量 I/O
ms.assetid: fc544776-af45-40e2-9699-7dcc50275d1e
keywords:
- IEEE 1394 WDK 总线，同步 I/O
- 1394 WDK 总线，同步 I/O
- I/O WDK IEEE 1394 总线
- I/O 请求数据包 WDK IEEE 1394 总线
- Irp WDK IEEE 1394 总线
- 同步 I/O WDK IEEE 1394 总线
- 有保证的带宽 WDK IEEE 1394 总线
- 带宽 WDK IEEE 1394 总线
- 同步 I/O WDK IEEE 1394 总线，有关同步 I/O
- 传输数据 WDK IEEE 1394 总线
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1f51c6ed708badb260aa34d715aa89ccc11df8a3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63371031"
---
# <a name="isochronous-io-for-ieee-1394-devices"></a>IEEE 1394 设备的常时等量 I/O





实时多媒体设备，如数字照相机需要大量的带宽在稳定流中发送数据，但不是需要有保证的传递。 （例如，从数字照相机丢弃的帧将会降低信号质量，但它不会销毁它的含义。）对于此类设备，提供 IEEE 1394*等时*传输，它提供有保证的带宽，但不保证传递。

本部分包括：

[设置同步传输的 IEEE 1394 设备](https://msdn.microsoft.com/library/windows/hardware/ff538108)

[缓冲等时 DMA 传输的 IEEE 1394 设备](https://msdn.microsoft.com/library/windows/hardware/ff537014)

[等时侦听的 IEEE 1394 设备的选项](https://msdn.microsoft.com/library/windows/hardware/ff537377)

[IEEE 1394 设备等时讨论选项](https://msdn.microsoft.com/library/windows/hardware/ff537380)

[适用于 IEEE 1394 设备同步的同步选项](https://msdn.microsoft.com/library/windows/hardware/ff537379)

[完成同步数据传输](https://msdn.microsoft.com/library/windows/hardware/ff537058)

 

 




