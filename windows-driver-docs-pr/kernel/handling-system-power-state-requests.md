---
title: 处理系统电源状态请求
description: 处理系统电源状态请求
ms.assetid: c4547b72-107e-4335-a7bd-081376962da0
keywords:
- 电源状态 WDK 内核
- 电源管理 WDK 内核，电源状态请求
- 系统电源状态 WDK 内核，电源状态请求
- 请求 WDK 电源管理
- Irp WDK 电源管理
- I/O 请求数据包 WDK 电源管理
- power 请求 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 85334d5348cfa4eac7a4ff357bbac2eb033bda9a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338525"
---
# <a name="handling-system-power-state-requests"></a>处理系统电源状态请求





所有驱动程序必须能够响应系统电源状态请求，如果系统睡眠、 休眠状态，并成功唤醒。 在设备发生更改的驱动程序[设备电源状态](device-power-states.md)系统电源状态请求的响应中的设备。

如果任何驱动程序不支持系统的电源管理，各个设备可以睡眠和唤醒，但电源管理器不能将系统作为一个整体置于休眠状态。

下列主题介绍了处理系统电源状态请求的详细信息：

[系统电源状态](system-power-states.md)

[系统电源策略](system-power-policy.md)

[阻止系统电源状态更改](preventing-system-power-state-changes.md)

[处理 IRP\_MN\_查询\_的电源可用于系统的电源状态](handling-irp-mn-query-power-for-system-power-states.md)

[处理 IRP\_MN\_设置\_的电源可用于系统的电源状态](handling-irp-mn-set-power-for-system-power-states.md)

 

 




