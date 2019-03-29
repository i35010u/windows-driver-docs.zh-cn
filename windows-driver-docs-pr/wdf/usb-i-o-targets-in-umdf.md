---
title: UMDF 中的 USB I/O 目标
description: UMDF 中的 USB I/O 目标
ms.assetid: e08ca910-1b28-4809-9a5b-db3730cda31a
keywords:
- 用户模式驱动程序 WDK UMDF，USB I/O 目标
- UMDF WDK，USB I/O 目标
- 用户模式驱动程序框架 WDK，USB I/O 目标
- 基于框架的驱动程序 WDK UMDF，USB I/O 目标
- USB I/O 面向 WDK UMDF
- I/O 目标 WDK UMDF USB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b91ec4da152a3bed45e272c96e6d4e26eae36f7d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576640"
---
# <a name="usb-io-targets-in-umdf"></a>UMDF 中的 USB I/O 目标

[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

每个通用串行总线 (USB) 设备和 USB 设备接口支持，每个管道都有单独的 I/O 目标。 USB 设备处理的 I/O 发送到设备的 I/O 目标。 特定的管道处理的 I/O 发送到该管道的 I/O 目标。

## <a name="in-this-section"></a>本节内容


-   [为 USB 设备选择驱动程序模型](choosing-a-driver-model-for-a-usb-device.md)
-   [特定于 USB 的 UMDF 1.x 接口](usb-specific-umdf-1-x-interfaces.md)
-   [使用 UMDF 1.x 驱动程序中的 USB 设备](working-with-usb-devices-in-umdf-1-x-drivers.md)
-   [使用 USB 接口在 UMDF 1.x 驱动程序](working-with-usb-interfaces-in-umdf-1-x-drivers.md)
-   [使用 USB 通过管道传入 UMDF 1.x 驱动程序](working-with-usb-pipes-in-umdf-1-x-drivers.md)
-   [通过 USB I/O 目标文件创建](file-creation-by-a-usb-i-o-target.md)
-   [从 UMDF 调用 WinUSB](escaping-to-winusb.md)

 

 





