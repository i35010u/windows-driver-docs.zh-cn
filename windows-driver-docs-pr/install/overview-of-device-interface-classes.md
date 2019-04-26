---
title: 设备接口类概述
description: 设备接口类概述
ms.assetid: e463e3f0-cbc8-490e-a7c4-4837d43c20e3
keywords:
- 接口类 WDK 设备安装
- 设备接口 WDK 设备安装
- 接口 WDK 设备
- 设备接口的类 WDK 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 60546d349fdad13ba3b59a6bead085cb1fd2e086
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330248"
---
# <a name="overview-of-device-interface-classes"></a>设备接口类概述





代码可将 I/O 请求定向到的用户模式的物理、 逻辑，或虚拟设备的任何驱动程序必须提供某种形式的名称及其用户模式下客户端。 使用的名称，在用户模式应用程序 （或其他系统组件） 标识，它从其请求 I/O 的设备。

在 Windows NT 4.0 和基于 NT 的操作系统的早期版本中，驱动程序名为其设备对象，然后设置符号链接，这些名称和用户可见的 Win32 逻辑名称之间在注册表中。

从 Windows 2000 开始，驱动程序未命名的设备对象。 相反，它们使利用*设备接口类*。 设备接口类是一种方法将设备和驱动程序功能导出到其他系统组件，包括其他驱动程序，以及用户模式应用程序。 驱动程序可以注册设备接口类，然后启用每个 I/O 请求可能会发送到的用户模式的设备对象的类的实例。

每个设备接口类是一个 GUID 与相关联。 系统定义的特定于设备的标头文件中的常见设备接口类的 Guid。 供应商可以创建其他设备接口的类。

例如，三个不同类型的鼠标设备可能是相同的设备接口类的成员，即使一个通过 USB 端口、 通过串行端口，第二个和第三个通过出红外端口连接。 每个驱动程序将其设备注册为接口类 GUID_DEVINTERFACE_MOUSE 的成员。 标头文件中定义此 GUID *Ntddmou.h*。

通常情况下，驱动程序注册，以便只有一个接口类。 但是，有专门的功能以外，为其标准接口，类定义的功能的设备的驱动程序可能也注册其他类。 例如，可以装载的磁盘的驱动程序应注册其磁盘接口类 (GUID_DEVINTERFACE_DISK) 和处于可装入设备类 (MOUNTDEV_MOUNTED_DEVICE_GUID)。

当驱动程序注册的设备接口类实例时，I/O 管理器将设备和设备接口类 GUID 关联的符号链接名称。 链接名称存储在注册表中，并会在系统启动中保留。 使用该接口的应用程序可以查询的接口的实例和接收表示支持的接口的设备的符号链接名称。 应用程序然后可以使用符号链接名称用作目标的 I/O 请求。

不要混淆设备驱动程序可以在响应中导出的接口与接口[ **IRP_MN_QUERY_INTERFACE** ](https://msdn.microsoft.com/library/windows/hardware/ff551687)请求。 该 IRP 用于内核模式驱动程序之间传递的例程的入口点。

 

 





