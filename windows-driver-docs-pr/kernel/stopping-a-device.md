---
title: 停止设备
description: 停止设备
ms.assetid: 65a47e7b-aabd-4b55-8fa6-c3482da1cc84
keywords:
- 停用该设备的即插即用 WDK 内核
- 停用该设备的即插 WDK 内核
- 停用该即插即用设备
- 停止 Irp WDK 即插即用
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b8b77eb3f3efd71dad0bea08d7fa1125c4eb599b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382978"
---
# <a name="stopping-a-device"></a>停止设备





PnP 管理器会提示停止在以下情况下的设备的驱动程序：

-   若要重新平衡正在使用设备的硬件资源。 重新平衡时通常需要枚举新设备时，需要已在使用资源。

-   若要禁用的设备管理器请求的响应中的设备 (Windows 98 / 只是我)。 Windows 2000 和更高版本的 Windows 发送这种情况下; 删除 Irp请参阅[了解当删除 Irp 将发出](understanding-when-remove-irps-are-issued.md)。

-   失败后[ **IRP\_MN\_启动\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)请求 (Windows 98 / 只是我)

本部分介绍以下主题：

[停止设备来重新平衡资源](stopping-a-device-to-rebalance-resources.md)

[停止以禁用它的设备 (Windows 98 / 我)](stopping-a-device-to-disable-it--windows-98-me-.md)

[停止后失败的启动设备 (Windows 98 / 我)](stopping-a-device-after-a-failed-start--windows-98-me-.md)

[处理停止 Irp (Windows 2000 及更高版本)](handling-stop-irps--windows-2000-and-later-.md)

[处理停止 Irp (Windows 98 / 我)](handling-stop-irps--windows-98-me-.md)

 

 




