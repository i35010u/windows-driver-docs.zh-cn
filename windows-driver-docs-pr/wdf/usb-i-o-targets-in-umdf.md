---
title: UMDF 中的 USB I/O 目标
description: UMDF 中的 USB I/O 目标
keywords:
- 用户模式驱动程序 WDK UMDF，USB i/o 目标
- UMDF WDK，USB i/o 目标
- User-Mode Driver Framework WDK，USB i/o 目标
- 基于框架的驱动程序 WDK UMDF，USB i/o 目标
- USB i/o 目标 WDK UMDF
- I/o 目标为 WDK UMDF、USB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d65e98cb459cf88e2ee4035f6a10b1c03facab6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824857"
---
# <a name="usb-io-targets-in-umdf"></a>UMDF 中的 USB I/O 目标

[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

每个通用串行总线 (USB) 设备和 USB 设备接口支持的每个管道都有单独的 i/o 目标。 USB 设备处理的 i/o 发送到设备的 i/o 目标。 特定管道进程发送到该管道的 i/o 目标的 i/o。

## <a name="in-this-section"></a>在本节中


-   [为 USB 设备选择驱动程序模型](choosing-a-driver-model-for-a-usb-device.md)
-   [特定于 USB 的 UMDF 1.x 接口](usb-specific-umdf-1-x-interfaces.md)
-   [在 UMDF 1.x 驱动程序中使用 USB 设备](working-with-usb-devices-in-umdf-1-x-drivers.md)
-   [在 UMDF 1.x 驱动程序中使用 USB 接口](working-with-usb-interfaces-in-umdf-1-x-drivers.md)
-   [在 UMDF 1.x 驱动程序中使用 USB 管道](working-with-usb-pipes-in-umdf-1-x-drivers.md)
-   [通过 USB I/O 目标创建文件](file-creation-by-a-usb-i-o-target.md)
-   [从 UMDF 调用 WinUSB](escaping-to-winusb.md)

 

 





