---
title: 使用设备接口
description: 使用设备接口
ms.assetid: a41f9ae2-6128-43e2-a6b5-4d0bd45371bd
keywords:
- 接口类 WDK 设备安装
- 设备接口的类 WDK 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec0ae9ba565aad37e6c5312ce6353bfb29d6ced2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339452"
---
# <a name="using-a-device-interface"></a>使用设备接口





设备接口可供内核模式组件和用户模式应用程序。 用户模式代码可以使用 **SetupDi * * * Xxx*函数要了解有关注册，启用设备接口。 请参阅[SetupDi 设备接口函数](using-device-installation-functions.md#ddk-setupdi-device-interface-functions-dg)有关详细信息。

内核模式组件可以使用特定设备或文件对象之前，它必须执行以下操作：

1.  确定是否已注册并启用所需的设备接口类。

    驱动程序可以注册 PnP 管理器中，若要启用或禁用设备接口的实例时收到通知。 若要注册的组件调用[ **IoRegisterPlugPlayNotification**](https://msdn.microsoft.com/library/windows/hardware/ff549526)。 此例程存储驱动程序所提供回调，每当设备接口实例的实例启用或禁用指定的设备类时调用的地址。 回调例程接收[ **DEVICE_INTERFACE_CHANGE_NOTIFICATION** ](https://msdn.microsoft.com/library/windows/hardware/ff543134)结构，其中包含表示接口实例的符号链接的 Unicode 字符串。 请参阅[使用即插即用设备接口更改通知](https://msdn.microsoft.com/library/windows/hardware/ff565474)有关详细信息。

    驱动程序或其他内核模式组件还可以调用[ **IoGetDeviceInterfaces** ](https://msdn.microsoft.com/library/windows/hardware/ff549186)若要获取列表的所有已注册，启用设备接口的特定设备接口类的新实例。 返回的列表包含指向标识设备接口实例的 Unicode 符号链接字符串。

2.  获取对应于接口的实例的设备或文件对象的指针。

    若要访问特定的设备对象，该驱动程序必须调用[ **IoGetDeviceObjectPointer**](https://msdn.microsoft.com/library/windows/hardware/ff549198)，并传递所需的接口中的 Unicode 字符串*ObjectName*参数。 若要访问的文件对象，该驱动程序必须调用[ **InitializeObjectAttributes**](https://msdn.microsoft.com/library/windows/hardware/ff547804)，将 Unicode 字符串中的传递*ObjectName*参数，，然后将传递成功初始化的调用中的属性结构[ **ZwCreateFile**](https://msdn.microsoft.com/library/windows/hardware/ff566424)。

 

 





