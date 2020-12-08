---
title: NT 设备名称
description: NT 设备名称
keywords:
- NT 设备名称 WDK 内核
- 设备对象 WDK 内核，名为
- 命名设备对象 WDK 内核
- 设备名称 WDK 内核
- 非 WDM 驱动程序设备名称 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2e9d7609740e5c860c445c8dadf662e75fd14ef0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837999"
---
# <a name="nt-device-names"></a>NT 设备名称





命名设备对象的名称为 **\\ \\ 设备**<em>DeviceName</em>。 这称为设备对象的 *NT 设备名称* 。

### <a name="device-names-for-wdm-drivers"></a>WDM 驱动程序的设备名称

WDM 驱动程序不会直接命名其设备对象。 相反，系统会实施统一的命名方案，以确保设备名称不会在驱动程序之间发生冲突。 WDM 驱动程序的命名方案如下所示。

-   设备的 PDO 命名为。 为其枚举的设备指定的总线驱动程序请求 PDOs。 总线驱动程序在 \_ 创建设备对象时指定文件自动生成的 \_ 设备 \_ 名称设备特性。 有关详细信息，请参阅 [指定设备特征](specifying-device-characteristics.md)。 然后，系统会自动生成设备名称。

-   FDOs 和筛选器 DOs 未命名。 函数和筛选器驱动程序在创建设备对象时不请求名称。

对命名设备对象的任何 i/o 请求会自动转到该设备对象堆栈中的顶层对象。 因此，只需将 PDO 命名为。 用户模式应用程序未按名称引用 WDM 设备对象;相反，应用程序通过其 *设备接口* 访问设备对象。 有关详细信息，请参阅 [设备接口类](../install/overview-of-device-interface-classes.md)。

驱动程序编写器不能在设备堆栈中命名多个对象。 操作系统基于命名对象检查安全设置。 如果两个不同的对象都命名为，并且具有不同的安全描述符，则使用较弱的安全描述符发送到对象的 i/o 请求可以访问具有更强安全描述符的设备对象。

### <a name="device-names-for-non-wdm-drivers"></a>非 WDM 驱动程序的设备名称

非 WDM 驱动程序必须为任何命名的设备对象显式指定名称。 驱动程序必须在 **\\ 设备** 对象目录中创建至少一个命名的设备对象来接收 i/o 请求。 创建设备对象时，驱动程序将设备名称指定为 [**IoCreateDeviceSecure**](/windows-hardware/drivers/ddi/wdmsec/nf-wdmsec-wdmlibiocreatedevicesecure)的 *DeviceName* 参数。

 

