---
title: 启动设备
description: 启动设备
ms.assetid: c52588cf-04c8-420d-a68e-a8754a65d546
keywords:
- 即插即用 WDK 内核，启动设备
- 即插即用和播放 WDK 内核，启动设备
- 启动即插即用设备
- DispatchPnP 例程
- IoCompletion 例程
- 启动 WDK 即插即用失败
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9614bfec6c95559a5ae08ba2b3f021e81d7a7957
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382991"
---
# <a name="starting-a-device"></a>启动设备





PnP 管理器将发送[ **IRP\_MN\_启动\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)以启动新枚举的设备，或重新启动现有设备的驱动程序请求停止以进行重新平衡资源。

函数和筛选器驱动程序必须设置[ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)例程，传递**IRP\_MN\_启动\_设备**关闭请求设备堆栈，并请其开始操作推迟到 IRP 用完所有较低的驱动程序。 父总线驱动程序设备堆栈中的底部驱动程序必须是第一个驱动程序的其他驱动程序访问该设备之前执行的设备上其开始操作。

若要确保正确序列化的开始操作，在 Windows 2000 和更高版本的 Windows 上的即插即用管理器推迟公开设备接口和块 IRP 成功开始创建设备的请求。

如果设备的驱动程序失败**IRP\_MN\_启动\_设备**请求，即插即用管理器将发送[ **IRP\_MN\_删除\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)设备堆栈 （在 Windows 2000 和更高版本的 Windows 上） 的请求。 在响应此 IRP，驱动程序的设备撤消其开始操作 （如果它们已成功开始 IRP），撤消其[ *AddDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)操作，并从设备堆栈中分离。 PnP 管理器将标记此类设备"失败开始"。

本部分介绍以下主题：

[功能驱动程序中启动设备](starting-a-device-in-a-function-driver.md)

[在筛选器驱动程序中启动设备](starting-a-device-in-a-filter-driver.md)

[总线驱动程序中启动设备](starting-a-device-in-a-bus-driver.md)

[用于启动设备的设计准则](design-guidelines-for-starting-devices.md)

 

 




