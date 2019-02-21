---
title: 处理 Power Irp 规则
description: 处理 Power Irp 规则
ms.assetid: ea4a1c57-6184-4160-bf23-b86e3e403388
keywords:
- 电源管理 WDK 内核 Irp
- Irp WDK 电源管理
- power Irp WDK 内核
- power Irp WDK 内核规则
- I/O 请求数据包 WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3b4bfb66815ed1a970e148b5e5839f8ba0e05e67
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542923"
---
# <a name="rules-for-handling-power-irps"></a>处理 Power Irp 规则





支持电源管理的驱动程序必须符合与相关的某些规则：

* [与调用 PoCallDriver 调用 IoCallDriver](calling-iocalldriver-versus-calling-pocalldriver.md)传递 power Irp

* [调用 PoStartNextPowerIrp](calling-postartnextpowerirp.md)启动下一个幂 IRP

* [传递 power Irp](passing-power-irps.md)向较低的下一步驱动程序

* [设备处于睡眠状态时排队的 I/O 请求](queuing-i-o-requests-while-a-device-is-sleeping.md)

* [处理不受支持或无法识别的 power Irp](handling-unsupported-or-unrecognized-power-irps.md)

* [处理能力 IRP 时调用 ExSetTimerResolution](calling-exsettimerresolution-while-processing-a-power-irp.md)

以下各节介绍如何驱动程序应执行这些任务。

电源管理 Irp 的列表，请参阅[电源管理次要 Irp](power-management-minor-irps.md)。

 




