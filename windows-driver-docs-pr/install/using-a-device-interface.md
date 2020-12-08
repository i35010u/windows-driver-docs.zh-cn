---
title: 使用设备接口
description: 使用设备接口
keywords:
- 接口类 WDK 设备安装
- 设备接口类 WDK 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 28ac9d72148565daf960dfc3644a958edf790cf1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827053"
---
# <a name="using-a-device-interface"></a>使用设备接口





设备接口可用于内核模式组件和用户模式应用程序。 用户模式代码可以使用 **SetupDi**_Xxx_ 函数来了解注册的已启用设备接口。 有关详细信息，请参阅 [SetupDi 设备接口功能](using-device-installation-functions.md#ddk-setupdi-device-interface-functions-dg) 。

在内核模式组件可以使用特定设备或文件对象之前，必须执行以下操作：

1.  确定是否注册并启用了所需的设备接口类。

    当启用或禁用设备接口的实例时，驱动程序可以向 PnP 管理器注册以获得通知。 若要注册，该组件将调用 [**IoRegisterPlugPlayNotification**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterplugplaynotification)。 此例程存储驱动程序提供的回调的地址，只要为指定的设备类启用或禁用了设备接口实例的实例，就会调用此回调。 回调例程接收 [**DEVICE_INTERFACE_CHANGE_NOTIFICATION**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_interface_change_notification) 结构，该结构包含表示接口实例的符号链接的 Unicode 字符串。 有关详细信息，请参阅 [使用 PnP 设备接口更改通知](../kernel/using-pnp-device-interface-change-notification.md) 。

    驱动程序或其他内核模式组件还可以调用 [**IoGetDeviceInterfaces**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceinterfaces) 来获取特定设备接口类的所有已注册的、已启用的设备接口实例的列表。 返回的列表包含指向标识设备接口实例的 Unicode 符号链接字符串的指针。

2.  获取一个指针，该指针指向与接口的实例相对应的设备或文件对象。

    若要访问特定设备对象，驱动程序必须调用 [**plxntb**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceobjectpointer)，并在 *ObjectName* 参数中传递所需接口的 Unicode 字符串。 若要访问文件对象，驱动程序必须调用 [**InitializeObjectAttributes**](/windows-hardware/drivers/ddi/wudfwdm/nf-wudfwdm-initializeobjectattributes)，在 *ObjectName* 参数中传递 Unicode 字符串，然后在对 [**ZwCreateFile**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntcreatefile)的调用中传递已成功初始化的属性结构。

