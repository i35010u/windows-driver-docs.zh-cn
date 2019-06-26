---
title: 发送等待/唤醒 IRP
description: 发送等待/唤醒 IRP
ms.assetid: ed582644-af51-4841-be59-6a3deb6d9de5
keywords:
- 电源管理 WDK 内核，唤醒功能
- 外部唤醒信号 WDK
- 唤醒设备
- 唤醒功能 WDK 电源管理
- 设备唤醒 ups WDK 电源管理
- IRP_MN_WAIT_WAKE
- 等待/唤醒 Irp WDK 电源管理发送
- 发送等待/唤醒 Irp
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: d7682bcbc0d2fc5327067d49bfb68620f1fd2253
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364086"
---
# <a name="sending-a-waitwake-irp"></a>发送等待/唤醒 IRP





次要 power IRP 代码[ **IRP\_MN\_等待\_唤醒**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake)提供用于唤醒设备或唤醒系统。 可以唤醒本身或系统的设备的驱动程序发送**IRP\_MN\_等待\_唤醒**请求。 系统发送**IRP\_MN\_等待\_唤醒**请求仅限为始终唤醒系统，例如电源开关的设备。

驱动程序发送**IRP\_MN\_等待\_唤醒**请求两个原因之一：

1.  其设备必须能够从睡眠状态，以外部唤醒信号的响应返回到工作状态。

    例如，调制解调器的驱动程序可能会发送它等待/唤醒 IRP 之前将其设置电源状态 D1 以节约能源。 等待/唤醒 IRP 使响应的传入呼叫的调制解调器。

2.  其设备必须能够响应唤醒信号将系统唤醒。

    调制解调器时系统进入睡眠状态，可能会保持与的 D1 状态**IRP\_MN\_等待\_唤醒**挂起。 在这种情况下，传入的呼叫将唤醒系统，以及调制解调器。

是否准备好设备唤醒本身或系统，其驱动程序必须执行的操作是相同的。 主要区别就在于设备和系统硬件如何响应初始唤醒信号。 驱动程序行为都是在任一情况下相同。

 

 




