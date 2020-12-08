---
title: 确定何时发送等待/唤醒 IRP
description: 确定何时发送等待/唤醒 IRP
keywords:
- 计时等待/唤醒 Irp WDK 电源管理
- 正在发送等待/唤醒 Irp
- 等待/唤醒 Irp WDK 电源管理，发送
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 01f1b0e9a07342b8885c6ba8f8f17098dcab2dbf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829551"
---
# <a name="determining-when-to-send-a-waitwake-irp"></a>确定何时发送等待/唤醒 IRP





拥有设备电源策略的驱动程序代表其设备发送等待/唤醒 Irp。 当出现下列情况之一时，此类驱动程序必须发送等待/唤醒 IRP：

-   驱动程序正在使设备进入睡眠状态，但设备必须能够唤醒，以响应外部唤醒信号。

-   系统将进入睡眠状态，并且设备必须能够对其唤醒。

电源策略所有者应发送等待/唤醒 IRP，然后再继续此类条件。 它可以在其设备处于 D0 时随时发送 IRP，但它在处理另一个设置电源或查询-电源 IRP 时不得发送此类 IRP。 作为一般规则，当驱动程序初始化并启动了设备之后，驱动程序应在处理即插即用 manager 的 [**irp \_ MN \_ START \_ 设备**](./irp-mn-start-device.md) 请求的过程中发送 IRP。

 

