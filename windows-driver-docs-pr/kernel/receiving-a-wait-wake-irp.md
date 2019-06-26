---
title: 接收等待/唤醒 IRP
description: 接收等待/唤醒 IRP
ms.assetid: 88fa7189-4897-484a-9cf4-b35e56e99d61
keywords:
- 电源管理 WDK 内核，唤醒功能
- 外部唤醒信号 WDK
- 唤醒设备
- 唤醒功能 WDK 电源管理
- 设备唤醒 ups WDK 电源管理
- IRP_MN_WAIT_WAKE
- 接收等待/唤醒 Irp
- 等待/唤醒 Irp WDK 电源管理，接收
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: dee40b223b5127136f23b8d83e9b25185f12ce80
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378740"
---
# <a name="receiving-a-waitwake-irp"></a>接收等待/唤醒 IRP





所有即插即用驱动程序必须准备好接收具有细微的 IRP 代码 power Irp [ **IRP\_MN\_等待\_唤醒**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake)。 驱动程序处理等待/唤醒 IRP 的方式取决于其设备堆栈，它控制的设备和从其其设备支持唤醒的特定状态的类型中的位置。

在本部分中的主题提供用于处理基于驱动程序的类型和其级别的等待/唤醒支持此 IRP 的指导原则。

 

 




