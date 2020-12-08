---
title: 支持具有唤醒功能的设备
description: 支持具有唤醒功能的设备
keywords:
- 电源管理 WDK 内核，唤醒功能
- 外部唤醒信号 WDK
- 唤醒设备
- 唤醒功能 WDK 电源管理
- 设备唤醒 ups WDK 电源管理
- IRP_MN_WAIT_WAKE
- 正在还原电源 WDK 内核
- Irp WDK 电源管理
- 等待/唤醒 Irp WDK 电源管理
- I/o 请求数据包 WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c230e473bf104358b37fa46ce2f0cf5de1ae8b9b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816633"
---
# <a name="supporting-devices-that-have-wake-up-capabilities"></a>支持具有唤醒功能的设备





可响应外部唤醒信号的设备的驱动程序必须能够处理 [**IRP \_ MN \_ 等待 \_ 唤醒**](./irp-mn-wait-wake.md) 请求 (*等待/唤醒 irp*) 。 此类设备的电源策略所有者必须能够发送 **IRP \_ MN \_ 等待 \_ 唤醒** 请求。

通常情况下，无论是什么原因，设备都可以断言唤醒信号。 例如，用户输入（可能导致键盘唤醒系统）是键盘及其驱动程序的正常事件。

本部分的第一个主题 " [等待/唤醒操作概述](overview-of-wait-wake-operation.md)" 包含有关编写任何驱动程序的有用信息。 以下其他主题提供了有关处理和发送 wait/唤醒 Irp 的详细信息：

[接收等待/唤醒 IRP](receiving-a-wait-wake-irp.md)

[发送等待/唤醒 IRP](sending-a-wait-wake-irp.md)

[取消等待/唤醒 IRP](canceling-a-wait-wake-irp.md)

 

