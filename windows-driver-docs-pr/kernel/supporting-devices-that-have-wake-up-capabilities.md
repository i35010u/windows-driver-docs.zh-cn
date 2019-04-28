---
title: 支持具有唤醒功能的设备
description: 支持具有唤醒功能的设备
ms.assetid: 70b9d0af-c3d7-44dc-b11a-3274391508c5
keywords:
- 电源管理 WDK 内核，唤醒功能
- 外部唤醒信号 WDK
- 唤醒设备
- 唤醒功能 WDK 电源管理
- 设备唤醒 ups WDK 电源管理
- IRP_MN_WAIT_WAKE
- 还原 power WDK 内核
- Irp WDK 电源管理
- 等待/唤醒 Irp WDK 电源管理
- I/O 请求数据包 WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 96ca29d334f077081fd4143bd449aceade882e81
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345435"
---
# <a name="supporting-devices-that-have-wake-up-capabilities"></a>支持具有唤醒功能的设备





可以响应外部唤醒信号的设备的驱动程序必须能够处理[ **IRP\_MN\_等待\_唤醒**](https://msdn.microsoft.com/library/windows/hardware/ff551766)请求 (*等待/唤醒Irp*)。 此类设备的电源策略所有者必须能够发送**IRP\_MN\_等待\_唤醒**请求。

通常情况下，任何会导致要声明唤醒信号的设备也是正常的服务事件的设备。 例如，用户输入，这可能会导致键盘来唤醒系统，是键盘，其驱动程序的正常事件。

本部分中，第一个主题[等待/唤醒操作概述](overview-of-wait-wake-operation.md)，包含在编写任何驱动程序的有用信息。 以下其他主题提供有关处理的详细的信息和发送等待/唤醒 Irp:

[接收等待/唤醒 IRP](receiving-a-wait-wake-irp.md)

[发送等待/唤醒 IRP](sending-a-wait-wake-irp.md)

[正在取消等待/唤醒 IRP](canceling-a-wait-wake-irp.md)

 

 




