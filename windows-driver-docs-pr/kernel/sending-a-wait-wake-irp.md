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
- 等待/唤醒 Irp WDK 电源管理，发送
- 正在发送等待/唤醒 Irp
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 33164b410fed940d7039f3f796cba6ae0baef641
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184399"
---
# <a name="sending-a-waitwake-irp"></a>发送等待/唤醒 IRP





次电源 IRP 代码 [**irp \_ MN \_ 等待 \_ 唤醒**](./irp-mn-wait-wake.md) 提供用于唤醒设备或唤醒系统。 可以自行唤醒或系统发送 **IRP \_ MN \_ 等待 \_ 唤醒** 请求的设备驱动程序。 系统仅将 **IRP \_ MN \_ 等待 \_ 唤醒** 请求发送到始终唤醒系统的设备，例如开机开关。

驱动程序出于以下两个原因之一发送 **IRP \_ MN \_ 等待 \_ 唤醒** 请求：

1.  其设备必须能够从睡眠状态返回到工作状态，以响应外部唤醒信号。

    例如，调制解调器的驱动程序可以在将其设置为电源状态 D1 之前向其发送等待/唤醒 IRP，以节省能源。 等待/唤醒 IRP 允许调制解调器响应传入呼叫。

2.  设备必须能够唤醒系统，以响应唤醒信号。

    当系统进入睡眠状态时，该调制解调器可能会保持与 **IRP \_ MN \_ 等待 \_ 唤醒** 挂起的状态 D1。 在这种情况下，传入调用会唤醒系统以及调制解调器。

无论设备是否准备好唤醒自身或系统，其驱动程序必须采用相同的操作。 主要区别在于设备和系统硬件对初始唤醒信号的响应方式。 在任一情况下，驱动程序行为都是相同的。

 

