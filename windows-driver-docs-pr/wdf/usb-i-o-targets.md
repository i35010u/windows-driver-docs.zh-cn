---
title: USB I/O 目标
description: 本部分介绍 KMDF 和 UMDF 2 驱动程序如何与通用串行总线 (USB) 设备进行交互。
ms.assetid: 195c0f4b-7f33-428a-8de7-32643ad854c6
keywords:
- I/O 目标 WDK KMDF USB
- USB I/O 面向 WDK KMDF
- USB 请求阻止 WDK KMDF
- URBs WDK KMDF
- USB I/O 面向 WDK KMDF 有关 USB I/O 目标
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 29069f3c74bf38b656045d9c00a621e92881fa4d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569496"
---
# <a name="usb-io-targets"></a>USB I/O 目标


本部分介绍从版本 2 的内核模式驱动程序框架 (KMDF) 和用户模式驱动程序框架 (UMDF) 驱动程序如何与通用串行总线 (USB) 设备进行交互。




每个 USB 设备和 USB 设备接口支持，每个管道都有单独的 I/O 目标。 控制传输的 USB 设备句柄发送到设备的 I/O 目标。 特定的管道处理的 I/O 传输发送到该管道的 I/O 目标。

通过发送 USB 请求块与 USB 设备的 I/O 目标通信框架 ([**URBs**](https://msdn.microsoft.com/library/windows/hardware/ff538923))。 该框架提供隐藏 URBs 从您的驱动程序，使驱动程序不需要生成并将其发送本身的对象方法。 如果您希望您的驱动程序生成 URBs，KMDF 驱动程序可以使用一组额外的生成和发送 URBs 对象方法。

有关如何确定 USB 设备需要哪种类型的驱动程序的信息，请参阅[选择用于开发 USB 客户端驱动程序的驱动程序模型](https://msdn.microsoft.com/library/windows/hardware/ff540215)。

本部分包括：

-   [使用 USB 设备](working-with-usb-devices.md)

-   [使用 USB 接口](working-with-usb-interfaces.md)

-   [使用 USB 管道](working-with-usb-pipes.md)

 

 





