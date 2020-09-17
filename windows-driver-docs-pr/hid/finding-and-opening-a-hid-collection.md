---
title: 找到并打开 HID 集合
description: 找到并打开 HID 集合
ms.assetid: b46fdb06-e6ae-4376-994f-69bf6539f2ce
keywords:
- 集合 WDK HID，查找
- HID 集合 WDK，查找
- 查找 HID 集合
- 集合 WDK HID，打开
- HID 集合 WDK，打开
- 打开 HID 集合
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bddc211bd972f93109c10b95a21e8e740e2f6ca5
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90715968"
---
# <a name="finding-and-opening-a-hid-collection"></a>找到并打开 HID 集合





本部分介绍用户模式的应用程序和内核模式驱动程序如何查找并打开顶级 [HID 集合](hid-collections.md)。

### <a name="user-mode-application"></a>用户模式应用程序

Microsoft Windows 提供了设备安装例程 ( **SetupDi * * * Xxx* 函数) 来查找和识别 HIDClass 设备。 Windows 提供了其他 Win32 函数以初始化并连接到 HID 集合。

在用户模式应用程序加载后，它将执行以下操作序列：

-   调用 [**HidD \_ GetHidGuid**](/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_gethidguid) 以获取 HIDClass 设备的系统定义的 GUID。

-   调用 [**SetupDiGetClassDevs**](/windows/win32/api/setupapi/nf-setupapi-setupdigetclassdevsw) 来获取不透明设备信息集的句柄，以描述系统中当前安装的所有 [HID 集合](hid-collections.md) 所支持的设备接口。 应用程序应 \_ \_ 在传递给**SetupDiGetClassDevs**的*Flags*参数中指定 DIGCF 和 DIGCF DEVICEINTERFACE。

-   重复调用 [**SetupDiEnumDeviceInterfaces**](/windows/win32/api/setupapi/nf-setupapi-setupdienumdeviceinterfaces) ，以检索所有可用的接口信息。

-   调用 [**SetupDiGetDeviceInterfaceDetail**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdeviceinterfacedetaila) 将每个集合的接口信息格式化为 SP \_ 接口 \_ 设备 \_ 详细信息 \_ 数据结构。 此结构的 **DevicePath** 成员包含应用程序在 Win32 函数 [**CreateFile**](/windows/win32/api/fileapi/nf-fileapi-createfilea) 中使用的用户模式名称，以获取 HID 集合的文件句柄。

-   调用 [**CreateFile**](/windows/win32/api/fileapi/nf-fileapi-createfilea) 以获取 HID 集合的文件句柄。

### <a name="kernel-mode-driver"></a>内核模式驱动程序

如果内核模式驱动程序是函数或筛选器驱动程序，则它会将设备对象附加到 HID 集合的设备堆栈。 驱动程序必须仅使用 create 请求来打开设备。

如果驱动程序不是函数或筛选器驱动程序，则它通常使用 [即插即用通知](../kernel/pnp-notification-overview.md) 来查找集合。 找到集合后，驱动程序将使用 create 请求打开该集合。

 

