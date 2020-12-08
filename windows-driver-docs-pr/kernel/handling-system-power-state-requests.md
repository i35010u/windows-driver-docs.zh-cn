---
title: 处理系统电源状态请求
description: 处理系统电源状态请求
keywords:
- 电源状态 WDK 内核
- 电源管理 WDK 内核，电源状态请求
- 系统电源状态 WDK 内核，电源状态请求
- 请求 WDK 电源管理
- Irp WDK 电源管理
- I/o 请求数据包 WDK 电源管理
- power requests WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: cff333d3addf06a776a3878d9da532c6388f332b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825635"
---
# <a name="handling-system-power-state-requests"></a>处理系统电源状态请求





如果系统处于休眠、休眠和唤醒状态，所有驱动程序都必须能够响应系统电源状态请求。 设备的驱动程序将更改设备的 [设备电源状态](device-power-states.md) 以响应系统电源状态请求。

如果任何驱动程序不支持系统电源管理，则单个设备可以睡眠并唤醒，但电源管理器无法将系统整体置于睡眠状态。

以下主题介绍处理系统电源状态请求的详细信息：

[系统电源状态](system-power-states.md)

[系统电源策略](system-power-policy.md)

[阻止系统电源状态更改](preventing-system-power-state-changes.md)

[处理 IRP \_ MN \_ QUERY \_ Power For System power 状态](handling-irp-mn-query-power-for-system-power-states.md)

[处理 IRP \_ MN \_ \_ 为系统电源状态设置电源](handling-irp-mn-set-power-for-system-power-states.md)

 

 




