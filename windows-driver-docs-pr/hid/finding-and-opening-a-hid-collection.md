---
title: 查找和打开 HID 集合
description: 查找和打开 HID 集合
ms.assetid: b46fdb06-e6ae-4376-994f-69bf6539f2ce
keywords:
- 集合 WDK HID 查找
- HID 的集合 WDK、 查找
- 查找 HID 集合
- WDK HID，打开的集合
- HID 的集合 WDK，打开
- 打开 HID 集合
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aaba2c5dfbfac7b488103a5e1388cf424b2ecb23
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554506"
---
# <a name="finding-and-opening-a-hid-collection"></a>查找和打开 HID 集合





本部分介绍如何用户模式应用程序和内核模式驱动程序查找和打开顶级[HID 集合](hid-collections.md)。

### <a name="user-mode-application"></a>用户模式应用程序

Microsoft Windows 提供的设备安装例程 (**SetupDi * * * Xxx*函数) 来查找和标识 HIDClass 设备。 Windows 提供了其他 Win32 函数以初始化并连接到 HID 集合。

在用户模式应用程序加载后，它将执行以下一系列操作：

-   调用[ **HidD\_GetHidGuid** ](https://msdn.microsoft.com/library/windows/hardware/ff538924)获取 HIDClass 设备的系统定义 GUID。

-   调用[ **SetupDiGetClassDevs** ](https://msdn.microsoft.com/library/windows/hardware/ff551069)若要获取的句柄描述所有支持的设备接口的不透明的设备信息集[HID 集合](hid-collections.md)当前安装在系统中。 应用程序应指定 DIGCF\_存在且 DIGCF\_中的 DEVICEINTERFACE*标志*参数传递给**SetupDiGetClassDevs**。

-   调用[ **SetupDiEnumDeviceInterfaces** ](https://msdn.microsoft.com/library/windows/hardware/ff551015)重复来检索所有可用的接口信息。

-   调用[ **SetupDiGetDeviceInterfaceDetail** ](https://msdn.microsoft.com/library/windows/hardware/ff551120)接口的信息的每个集合作为 SP\_接口\_设备\_详细\_数据结构。 **DevicePath**此结构的成员包含应用程序使用使用 Win32 函数的用户模式名称[ **CreateFile** ](https://msdn.microsoft.com/library/windows/desktop/aa363858)若要获取的文件句柄 HID集合。

-   调用[ **CreateFile** ](https://msdn.microsoft.com/library/windows/desktop/aa363858)若要获取的文件句柄 HID 集合。

### <a name="kernel-mode-driver"></a>Kernel-Mode Driver

如果内核模式驱动程序是一个函数或筛选器驱动程序，它已附加到 HID 集合设备堆栈的一个设备对象。 该驱动程序必须仅使用创建请求以打开设备。

如果该驱动程序不是函数或筛选器驱动程序，它通常会使用[即插即用通知](https://msdn.microsoft.com/library/windows/hardware/ff559640)查找集合。 找到后集合，该驱动程序使用创建请求打开集合。

 

 




