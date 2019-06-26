---
title: 即插即用管理器
description: 即插即用管理器
ms.assetid: b1890b3c-fc7b-4a2e-b48a-8266f237c9b6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 94c08fb3952610b2363e22f4c5ef65497339fd90
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360833"
---
# <a name="plug-and-play-manager"></a>即插即用管理器


Plug and Play (PnP) 管理器中 Windows 即插即用功能提供支持，并负责以下 PnP 相关的任务：

-   设备检测和枚举期间启动系统

-   添加或删除设备，系统运行时

新设备的系统上存在并且必须安装，内核模式即插即用管理器将通知用户模式即插即用管理器。

内核模式即插即用管理器还会调用[ *DriverEntry* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)并[ *AddDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)例程的设备的驱动程序，并将发送[**执行了 IRP_MN_START_DEVICE** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)启动设备的请求。

PnP 管理器维护[设备树](https://docs.microsoft.com/windows-hardware/drivers/kernel/device-tree)，会跟踪系统中的设备。 设备树包含系统上存在的设备的相关信息。 在计算机启动时，PnP 管理器使用的驱动程序和其他组件的信息生成此树，并更新树，如添加或删除设备。

 

 





