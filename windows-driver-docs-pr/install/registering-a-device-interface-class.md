---
title: 注册设备接口类
description: 注册设备接口类
ms.assetid: 1518570d-1cfb-498e-91f7-35f9cc11aff5
keywords:
- 接口类 WDK 设备安装
- 注册设备接口类
- 设备接口类 WDK 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 26a2a14777eb9158ffb1284bc6169ec9f255f650
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837371"
---
# <a name="registering-a-device-interface-class"></a>注册设备接口类





有三种方法可以注册设备接口类：

-   内核模式组件（如大多数驱动程序）可以调用 i/o 管理器例程。 本主题介绍如何使用这些例程。

-   用户模式*设备安装应用程序*调用 **SetupDi * * * Xxx*函数。 有关这些函数的详细信息，请参阅[SetupDi 设备接口函数](using-device-installation-functions.md#ddk-setupdi-device-interface-functions-dg)。

-   INF 文件可以包含[**Inf DDInstall 部分**](inf-ddinstall-interfaces-section.md)。

WDM 驱动程序不会为其设备对象命名。 相反，当驱动程序调用[**IoCreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice)来创建设备对象时，它应为设备名称指定一个空字符串。 有关详细信息，请参阅[创建设备对象](https://docs.microsoft.com/windows-hardware/drivers/kernel/creating-a-device-object)。

创建设备对象并将其附加到设备堆栈后，一个驱动程序调用[**IoRegisterDeviceInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterdeviceinterface)来注册设备接口类并创建接口的实例。 通常，函数驱动程序从其[**AddDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)例程进行此调用，但有时筛选器驱动程序会注册接口。

例程返回符号链接名称。 当驱动程序启用或禁用设备接口实例时，它会传递链接名称。 在驱动程序启用设备接口实例之前，其他系统组件不能使用该实例。 有关详细信息，请参阅[启用和禁用设备接口实例](enabling-and-disabling-a-device-interface-instance.md)。

驱动程序还使用符号链接名称来访问注册表项，该注册表项可以存储特定于设备接口的信息。 （有关详细信息，请参阅[**IoOpenDeviceInterfaceRegistryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioopendeviceinterfaceregistrykey) 。）应用程序使用链接名称打开设备。

驱动程序可根据需要多次调用[**IoRegisterDeviceInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterdeviceinterface)以注册其他设备接口类的实例。

 

 





