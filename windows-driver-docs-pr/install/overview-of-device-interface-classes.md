---
title: 设备接口类概述
description: 设备接口类概述
keywords:
- 接口类 WDK 设备安装
- 设备接口 WDK 设备安装
- 接口 WDK 设备
- 设备接口类 WDK 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0ac6fa5acd8ecc068d21cfeb93b949ae177ba582
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810009"
---
# <a name="overview-of-device-interface-classes"></a>设备接口类概述





用户模式代码可以将 i/o 请求定向到的物理、逻辑或虚拟设备的任何驱动程序都必须为其用户模式客户端提供某种类型的名称。 使用该名称时，用户模式应用程序 (或其他系统组件) 会标识向其发出 i/o 请求的设备。

在 Windows NT 4.0 和更早版本的基于 NT 的操作系统中，驱动程序命名为其设备对象，然后在这些名称与用户可见的 Win32 逻辑名称之间的注册表中设置符号链接。

从 Windows 2000 开始，驱动程序不命名设备对象。 相反，它们使用 *设备接口类*。 设备接口类是一种将设备和驱动程序功能导出到其他系统组件的方法，包括其他驱动程序和用户模式应用程序。 驱动程序可以注册一个设备接口类，然后为每个可能发送用户模式 i/o 请求的设备对象启用类的实例。

每个设备接口类都与一个 GUID 关联。 系统为特定于设备的标头文件中的常见设备接口类定义 Guid。 供应商可以创建其他设备接口类。

例如，三种不同类型的鼠标设备可以是同一设备接口类的成员，即使一个设备是通过 USB 端口连接，另一个通过串行端口，第三个则通过红外端口。 每个驱动程序将其设备注册为 GUID_DEVINTERFACE_MOUSE 接口类的成员。 此 GUID 在头文件 *Ntddmou* 中定义。

通常，驱动程序只注册一个接口类。 但是，如果设备的驱动程序的专用功能超出为其标准接口类定义的功能，则可能还会注册其他类。 例如，可以装入的磁盘的驱动程序应注册其磁盘接口类 (GUID_DEVINTERFACE_DISK) 和可装入设备类 (MOUNTDEV_MOUNTED_DEVICE_GUID) 。

当驱动程序注册设备接口类的实例时，i/o 管理器会将设备和设备接口类 GUID 与符号链接名称关联起来。 链接名称存储在注册表中，并在系统启动时保持。 使用接口的应用程序可以查询接口的实例，并接收表示支持接口的设备的符号链接名称。 然后，应用程序可以使用符号链接名称作为 i/o 请求的目标。

不要将设备接口与驱动程序可以导出以响应 [**IRP_MN_QUERY_INTERFACE**](../kernel/irp-mn-query-interface.md) 请求的接口混淆。 该 IRP 用于在内核模式驱动程序之间传递例程入口点。

 

