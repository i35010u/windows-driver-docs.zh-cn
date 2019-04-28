---
title: 注册设备接口类
description: 注册设备接口类
ms.assetid: 1518570d-1cfb-498e-91f7-35f9cc11aff5
keywords:
- 接口类 WDK 设备安装
- 注册设备接口类
- 设备接口的类 WDK 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b5fd58a579fbdbc46dbfc82f87ef8d88953397c8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348179"
---
# <a name="registering-a-device-interface-class"></a>注册设备接口类





有三种方法，以注册设备接口类：

-   内核模式组件，如大多数驱动程序，可以调用 I/O 管理器例程。 本主题介绍如何使用这些例程。

-   用户模式下*设备安装应用程序*调用 **SetupDi * * * Xxx*函数。 有关这些函数的详细信息，请参阅[SetupDi 设备接口函数](using-device-installation-functions.md#ddk-setupdi-device-interface-functions-dg)。

-   INF 文件可以包含[ **INF DDInstall.Interfaces 部分**](inf-ddinstall-interfaces-section.md)。

WDM 驱动程序没有命名其设备对象。 相反，当驱动程序调用[ **IoCreateDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff548397)若要创建一个设备对象，还应指定设备名称的空字符串。 有关详细信息，请参阅[创建一个设备对象](https://msdn.microsoft.com/library/windows/hardware/ff542862)。

创建设备对象并将其附加到设备堆栈后, 一个驱动程序调用[ **IoRegisterDeviceInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff549506)以注册设备接口类并创建接口的实例。 通常情况下，函数驱动程序，可以从此调用其[ **AddDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff540521)例程，但有时筛选器驱动程序注册接口。

例程将返回一个符号链接名称。 驱动程序时启用或禁用设备接口实例，请将链接名称。 其他系统组件不能使用设备接口实例，直到该驱动程序已启用该功能。 请参阅[启用和禁用设备接口实例](enabling-and-disabling-a-device-interface-instance.md)有关详细信息。

该驱动程序还使用符号链接名称来访问注册表项，它可以在其中存储特定于设备接口的信息。 (请参阅[ **IoOpenDeviceInterfaceRegistryKey** ](https://msdn.microsoft.com/library/windows/hardware/ff549433)有关详细信息。)应用程序使用的链接名称以打开设备。

驱动程序可以调用[ **IoRegisterDeviceInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff549506)尽可能多地需要注册其他设备接口类的实例。

 

 





