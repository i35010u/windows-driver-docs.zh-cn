---
title: 即插即用管理器
description: 即插即用管理器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 02bc4eb220a4d85eb1699a451cabcdda3219091a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827059"
---
# <a name="plug-and-play-manager"></a>即插即用管理器


即插即用 (PnP) 管理器提供对 Windows 中 PnP 功能的支持，并负责执行以下与 PnP 相关的任务：

-   系统启动时的设备检测和枚举

-   在系统运行时添加或删除设备

内核模式 PnP 管理器向用户模式 PnP 管理器通知系统上存在新设备，必须安装该设备。

内核模式 PnP 管理器还会调用设备驱动程序的 [*DriverEntry*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize) 和 [*AddDevice*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device) 例程，并发送 [**IRP_MN_START_DEVICE**](../kernel/irp-mn-start-device.md) 请求来启动设备。

PnP 管理器维护在系统中跟踪设备的 [设备树](../kernel/device-tree.md) 。 设备树包含有关系统上的设备的信息。 计算机启动时，PnP 管理器使用驱动程序和其他组件中的信息生成此树，并在添加或删除设备时更新树。

 

