---
title: USB I/O 目标
description: 本部分介绍了 KMDF 和 UMDF 2 驱动程序如何与通用串行总线 (USB) 设备交互。
ms.assetid: 195c0f4b-7f33-428a-8de7-32643ad854c6
keywords:
- I/o 目标 WDK KMDF，USB
- USB i/o 目标 WDK KMDF
- USB 请求块 WDK KMDF
- URBs WDK KMDF
- USB i/o 目标 WDK KMDF，关于 USB i/o 目标
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 158c2dd17f7e46d14df7b54f43968e47b4326a79
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89185303"
---
# <a name="usb-io-targets"></a>USB I/O 目标


本部分介绍内核模式驱动程序框架 (KMDF) 和用户模式驱动程序框架 (UMDF) 从版本2开始的驱动程序如何与通用串行总线 (USB) 设备交互。




每个 USB 设备以及 USB 设备接口支持的每个管道都具有单独的 i/o 目标。 将 USB 设备处理的控制传输发送到设备的 i/o 目标。 I/o 会传输特定管道句柄发送到该管道的 i/o 目标。

此框架通过发送 USB 请求块 ([**URBs**](/windows-hardware/drivers/ddi/usb/ns-usb-_urb)) ，与 usb 设备的 i/o 目标通信。 该框架提供了对象方法，这些方法可隐藏驱动程序中的 URBs，以便驱动程序无需生成并发送自身。 如果希望驱动程序生成 URBs，KMDF 驱动程序可以使用一组额外的对象方法来生成和发送 URBs。

有关如何确定 USB 设备所需的驱动程序类型的信息，请参阅 [选择用于开发 usb 客户端驱动](/windows-hardware/drivers/ddi/index)程序的驱动程序模型。

本节包括：

-   [使用 USB 设备](working-with-usb-devices.md)

-   [使用 USB 接口](working-with-usb-interfaces.md)

-   [使用 USB 管道](working-with-usb-pipes.md)

 

