---
title: 磁带驱动程序
description: 磁带驱动程序
ms.assetid: d6d8ac92-0713-401c-9551-fc8e08e903f4
keywords:
- 磁带驱动程序 WDK 存储
- 存储磁带驱动程序 WDK
- 存储驱动程序 WDK，磁带驱动程序
- 磁带驱动程序 WDK 存储有关磁带驱动程序
- 存储磁带驱动程序 WDK，有关磁带驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 675b243123df0199db857a1291f9a3d975befe84
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386808"
---
# <a name="tape-drivers"></a>磁带驱动程序


## <span id="ddk_tape_drivers_kg"></span><span id="DDK_TAPE_DRIVERS_KG"></span>


本部分包含以下信息：

[使用磁带类驱动程序](using-the-tape-class-driver.md)

[必需和可选磁带 Miniclass 例程](required-and-optional-tape-miniclass-routines.md)

[将磁带 Miniclass 上下文存储在可选扩展](storing-tape-miniclass-context-in-optional-extensions.md)

[处理磁带设备控制请求](processing-tape-device-control-requests.md)

基于 NT 的操作系统提供的泛型磁带类驱动程序，处理特定于操作系统和设备无关的磁带的任务。 作为内核模式 DLL 提供磁带类驱动程序。 若要支持新的磁带设备或磁带设备系列，驱动程序编写器创建特定于设备的磁带 miniclass 驱动程序动态地向系统提供磁带类驱动程序链接。

如果磁带 miniclass 驱动程序中的磁带类驱动程序调用仅例程，miniclass 驱动程序可以在可移植整个 Microsoft 操作系统的支持 Win32 应用程序，并提供使用磁带 miniclass 接口的磁带类驱动程序。 磁带 miniclass 驱动程序包含头文件*minitape.h*。

必须修改现有磁带 miniclass 驱动程序，以支持一个新入口点，TapeMiniGetMediaTypes，才能生成和运行 Windows 2000 和更高版本操作系统下。 不不需要任何其他修改。 在系统提供磁带类驱动程序，以及系统提供的存储端口驱动程序、 句柄插和代表磁带 miniclass 驱动程序的电源管理请求。

本部分介绍特定于操作系统的磁带类驱动程序提供的支持，并为编写新的磁带 miniclass 驱动程序提供了指导原则。 请参阅[磁带类驱动程序例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)并[磁带 Miniclass 驱动程序例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)磁带中的例程的详细信息类和磁带 miniclass 驱动程序。 请参阅[设备的配置和层的驱动程序](https://docs.microsoft.com/windows-hardware/drivers/kernel/device-configurations-and-layered-drivers)有关存储设备驱动程序层的说明。

 

 




