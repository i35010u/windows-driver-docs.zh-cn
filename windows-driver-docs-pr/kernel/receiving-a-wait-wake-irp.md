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
- 正在接收等待/唤醒 Irp
- 等待/唤醒 Irp WDK 电源管理，接收
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2ec24fd70c64a36b354d2362865e17919cfbc003
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186221"
---
# <a name="receiving-a-waitwake-irp"></a>接收等待/唤醒 IRP





所有 PnP 驱动程序必须准备好接收具有次要 IRP 代码 [**irp \_ MN \_ 等待 \_ 唤醒**](./irp-mn-wait-wake.md)的电源 irp。 驱动程序处理等待/唤醒 IRP 的方式取决于其在设备堆栈中的位置、设备的类型 () 控制的类型，以及设备支持唤醒的特定状态。

本节中的主题提供了有关基于驱动程序类型及其等待/唤醒支持级别处理此 IRP 的指导原则。

 

