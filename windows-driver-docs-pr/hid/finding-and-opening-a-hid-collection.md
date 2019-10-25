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
ms.openlocfilehash: 025bb988eb7d61d5eb060e5b45bf918c58daadcc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824815"
---
# <a name="finding-and-opening-a-hid-collection"></a>找到并打开 HID 集合





本部分介绍用户模式的应用程序和内核模式驱动程序如何查找并打开顶级[HID 集合](hid-collections.md)。

### <a name="user-mode-application"></a>用户模式应用程序

Microsoft Windows 提供了设备安装例程（**SetupDi * ** ）来查找和识别 HIDClass 设备。 Windows 提供了其他 Win32 函数以初始化并连接到 HID 集合。

在用户模式应用程序加载后，它将执行以下操作序列：

-   调用[**HidD\_GetHidGuid**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_gethidguid)为 HIDClass 设备获取系统定义的 GUID。

-   调用[**SetupDiGetClassDevs**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassdevsw)来获取不透明设备信息集的句柄，以描述系统中当前安装的所有[HID 集合](hid-collections.md)所支持的设备接口。 应用程序应在传递给**SetupDiGetClassDevs**的*Flags*参数中指定 DIGCF\_存在并且 DIGCF\_DEVICEINTERFACE。

-   重复调用[**SetupDiEnumDeviceInterfaces**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdienumdeviceinterfaces) ，以检索所有可用的接口信息。

-   调用[**SetupDiGetDeviceInterfaceDetail**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinterfacedetaila)将每个集合的接口信息格式设置为 SP\_接口\_设备\_详细信息\_数据结构。 此结构的**DevicePath**成员包含应用程序在 Win32 函数[**CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)中使用的用户模式名称，以获取 HID 集合的文件句柄。

-   调用[**CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)以获取 HID 集合的文件句柄。

### <a name="kernel-mode-driver"></a>内核模式驱动程序

如果内核模式驱动程序是函数或筛选器驱动程序，则它会将设备对象附加到 HID 集合的设备堆栈。 驱动程序必须仅使用 create 请求来打开设备。

如果驱动程序不是函数或筛选器驱动程序，则它通常使用[即插即用通知](https://docs.microsoft.com/windows-hardware/drivers/kernel/pnp-notification-overview)来查找集合。 找到集合后，驱动程序将使用 create 请求打开该集合。

 

 




