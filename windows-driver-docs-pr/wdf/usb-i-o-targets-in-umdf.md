---
title: UMDF 中的 USB I/O 目标
description: UMDF 中的 USB I/O 目标
ms.assetid: e08ca910-1b28-4809-9a5b-db3730cda31a
keywords:
- 用户模式驱动程序 WDK UMDF，USB i/o 目标
- UMDF WDK，USB i/o 目标
- 用户模式驱动程序框架 WDK，USB i/o 目标
- 基于框架的驱动程序 WDK UMDF，USB i/o 目标
- USB i/o 目标 WDK UMDF
- I/o 目标为 WDK UMDF、USB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9bc4340371a0c9d68227d9ea9c3e731812c593f8
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210773"
---
# <a name="usb-io-targets-in-umdf"></a>UMDF 中的 USB I/O 目标

[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

每个通用串行总线（USB）设备和 USB 设备接口支持的每个管道都具有单独的 i/o 目标。 USB 设备处理的 i/o 发送到设备的 i/o 目标。 特定管道进程发送到该管道的 i/o 目标的 i/o。

## <a name="in-this-section"></a>本部分内容


-   [为 USB 设备选择驱动程序型号](choosing-a-driver-model-for-a-usb-device.md)
-   [USB 特定的 UMDF 1.x 接口](usb-specific-umdf-1-x-interfaces.md)
-   [在 UMDF 1.x 驱动程序中使用 USB 设备](working-with-usb-devices-in-umdf-1-x-drivers.md)
-   [在 UMDF 1.x 驱动程序中使用 USB 接口](working-with-usb-interfaces-in-umdf-1-x-drivers.md)
-   [在 UMDF 1.x 驱动程序中使用 USB 管道](working-with-usb-pipes-in-umdf-1-x-drivers.md)
-   [通过 USB i/o 目标创建文件](file-creation-by-a-usb-i-o-target.md)
-   [从 UMDF 调用 WinUSB](escaping-to-winusb.md)

 

 





