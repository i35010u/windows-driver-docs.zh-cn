---
title: 即插即用管理器
description: 即插即用管理器
ms.assetid: b1890b3c-fc7b-4a2e-b48a-8266f237c9b6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3fdd2151ae2d6027730d3546aff06a8b714df118
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837382"
---
# <a name="plug-and-play-manager"></a>即插即用管理器


即插即用（PnP）管理器为 Windows 中的 PnP 功能提供支持，并负责执行以下与 PnP 相关的任务：

-   系统启动时的设备检测和枚举

-   在系统运行时添加或删除设备

内核模式 PnP 管理器向用户模式 PnP 管理器通知系统上存在新设备，必须安装该设备。

内核模式 PnP 管理器还会调用设备驱动程序的[*DriverEntry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)和[*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)例程，并发送[**IRP_MN_START_DEVICE**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)请求来启动设备。

PnP 管理器维护在系统中跟踪设备的[设备树](https://docs.microsoft.com/windows-hardware/drivers/kernel/device-tree)。 设备树包含有关系统上的设备的信息。 计算机启动时，PnP 管理器使用驱动程序和其他组件中的信息生成此树，并在添加或删除设备时更新树。

 

 





