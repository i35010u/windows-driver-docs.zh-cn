---
title: 确定何时发送等待/唤醒 IRP
description: 确定何时发送等待/唤醒 IRP
ms.assetid: a56cfccc-b44b-4ec5-836b-3a9711ef5f1f
keywords:
- 计时等待/唤醒 Irp WDK 电源管理
- 发送等待/唤醒 Irp
- 等待/唤醒 Irp WDK 电源管理发送
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 13bcd0548c378c0d47aad223cd2f363198fc636b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371263"
---
# <a name="determining-when-to-send-a-waitwake-irp"></a>确定何时发送等待/唤醒 IRP





拥有设备的电源策略发送的驱动程序等待/唤醒 Irp 代表其设备。 以下项之一发生时，此类驱动程序必须发送等待/唤醒 IRP:

-   该驱动程序会让设备进入睡眠状态，但该设备必须能够响应外部唤醒信号中唤醒。

-   系统将进入睡眠状态，设备必须能够唤醒它。

电源策略所有者应发送等待/唤醒 IRP，这种情况是即将之前。 它可以发送的 IRP 随时其设备处于 D0，但不是能发送此类的 IRP 时它正在处理另一组 power 或查询能耗 IRP。 作为一般规则，驱动程序应将发送 IRP 插 manager 其处理期间[ **IRP\_MN\_启动\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)请求，它具有后初始化和启动设备。

 

 




