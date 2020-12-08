---
title: IEEE 1394 设备的常时等量 I/O
description: IEEE 1394 设备的常时等量 I/O
keywords:
- IEEE 1394 WDK 总线，同步 i/o
- 1394 WDK 总线，同步 i/o
- I/o WDK IEEE 1394 总线
- I/o 请求数据包 WDK IEEE 1394 总线
- Irp WDK IEEE 1394 总线
- 同步 i/o WDK IEEE 1394 总线
- 保证带宽 WDK IEEE 1394 总线
- 带宽 WDK IEEE 1394 总线
- 同步 i/o WDK IEEE 1394 总线，关于同步 i/o
- 传输数据 WDK IEEE 1394 总线
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17e3753e0384c3166bc4a75fb82a9349d79009e0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805601"
---
# <a name="isochronous-io-for-ieee-1394-devices"></a>IEEE 1394 设备的常时等量 I/O





诸如数码相机这样的实时多媒体设备需要大量带宽才能以稳定流的形式发送数据，但不需要确保送达。  (例如，从数字照相机拖放的帧会降低信号的质量，但不会损坏其含义。 ) 对于此类设备，IEEE 1394 提供按 *流量传输，可提供有* 保证的带宽，但不保证送达。

本节包括：

[设置 IEEE 1394 设备的常时等量传输](./setting-up-isochronous-transfer-for-ieee-1394-devices.md)

[缓冲 IEEE 1394 设备的常时等量 DMA 传输](./buffering-isochronous-dma-transfers-for-ieee-1394-devices.md)

[IEEE 1394 设备的常时等量侦听选项](./isochronous-listen-options-for-ieee-1394-devices.md)

[IEEE 1394 设备的常时等量交谈选项](./isochronous-talk-options-for-ieee-1394-devices.md)

[IEEE 1394 设备的常时等量同步选项](./isochronous-synchronization-options-for-ieee-1394-devices.md)

[完成常时等量数据传输](./completing-an-isochronous-data-transfer.md)

 

