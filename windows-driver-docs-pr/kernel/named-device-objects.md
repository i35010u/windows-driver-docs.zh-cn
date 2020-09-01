---
title: 命名的设备对象
description: 命名的设备对象
ms.assetid: 4e24f0c1-57b2-4e06-a7f5-9a93d365ac8c
keywords:
- 设备对象 WDK 内核，名为
- 命名设备对象 WDK 内核
ms.date: 09/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15920ed802426f7a50760cf1a4f92ffe09613e9d
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89187911"
---
# <a name="named-device-objects"></a>命名的设备对象





与所有对象管理器对象一样，设备对象可以命名或未命名。 用户模式应用程序发出 i/o 请求时，它会按名称指定操作的目标。 对象管理器解析该名称以确定 i/o 请求的目标。

> [!IMPORTANT]
> 仅在必要时帮助增加驱动程序安全名称设备对象。 命名设备对象通常只是出于传统原因所必需的，例如，如果应用程序需要使用特定的名称打开设备，或者使用非 PNP 设备/控制设备。  请注意，WDF 驱动程序无需命名其 PnP 设备，就可以使用 [WdfDeviceCreateSymbolicLink](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreatesymboliclink)创建符号链接。

驱动程序可以在调用 [**IoCreateDevice**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice) 或 [**IoCreateDeviceSecure**](/windows-hardware/drivers/ddi/wdmsec/nf-wdmsec-wdmlibiocreatedevicesecure) 来创建设备对象时，为设备对象指定一个名称。 有关何时以及如何命名设备对象的详细信息，请参阅 [NT 设备名称](nt-device-names.md)。
  
命名设备对象还可以具有 MS-DOS 设备名称，这是由 [**IoCreateSymbolicLink**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatesymboliclink) 或 [**IoCreateUnprotectedSymbolicLink**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreateunprotectedsymboliclink)创建的符号链接。 WDM 驱动程序通常不需要 MS-DOS 设备名称。 有关详细信息，请参阅 [MS-DOS 设备名称](ms-dos-device-names.md)。

> [!IMPORTANT]
> 如果使用命名设备对象，则可以使用 [IoCreateDeviceSecure](/windows-hardware/drivers/ddi/wdmsec/nf-wdmsec-wdmlibiocreatedevicesecure) 并指定 SDDL 来帮助保护该对象。 实现 [IoCreateDeviceSecure](/windows-hardware/drivers/ddi/wdmsec/nf-wdmsec-wdmlibiocreatedevicesecure) 时，请始终指定 DeviceClassGuid 的自定义类 GUID。 不应在此指定现有的类 GUID。 这样做可能会中断属于该类的其他设备的安全设置或兼容性。 有关详细信息，请参阅 [WdmlibIoCreateDeviceSecure](/windows-hardware/drivers/ddi/wdmsec/nf-wdmsec-wdmlibiocreatedevicesecure)。
> 
> 为了使应用程序或其他 WDF 驱动程序能够访问 PnP 设备，你应该使用设备接口。 有关详细信息，请参阅 [使用设备接口](../wdf/using-device-interfaces.md)。 设备接口用作设备堆栈 PDO 的符号链接。 一旦控制对 PDO 的访问权限，就可以在 INF 中指定一个 SDDL 字符串。 如果 SDDL 字符串不在 INF 文件中，则 Windows 将应用默认安全描述符。 有关详细信息，请参阅[为设备](./sddl-for-device-objects.md)对象[保护设备对象](https://docs.microsoft.com/windows-hardware/drivers/kernel/securing-device-objects)和 SDDL。


本部分包含以下小节：

[NT 设备名称](nt-device-names.md)

[MS-DOS 设备名称](ms-dos-device-names.md)

 

