---
title: 确定正确的设备电源状态
description: 确定正确的设备电源状态
ms.assetid: 4acefe93-1d7a-4c12-8701-03c2a8929591
keywords:
- DEVICE_CAPABILITIES 结构
- 更正设备电源状态 WDK 电源管理
- 设备电源状态 WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6f3891c9a4cb775be0a4071d402ec01f0719d4f4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836940"
---
# <a name="determining-the-correct-device-power-state"></a>确定正确的设备电源状态





电源策略所有者检查[**设备\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)结构中的[**DeviceState**](devicestate.md)阵列，以确定每个系统电源状态的设备电源状态的有效范围。 阵列列出了基础设备可以支持的每个系统电源状态的最高设备电源状态。

从此范围选择特定状态时，请考虑以下事项：

-   大多数设备在系统进入 S0 状态时进入 D0 状态。

-   大多数设备在系统进入任何休眠状态时进入 D3 状态。 但是，启用了唤醒功能的设备可能需要输入 D1 或 D2，如果它支持此类状态。 有关详细信息，请参阅[报表设备功能](reporting-device-power-capabilities.md)。

-   特殊规则适用于将保存休眠文件的设备。 如果系统 IRP 请求**PowerSystemHibernate**，则保存休眠文件的设备不得关闭电源。 此类设备的电源策略所有者应该请求设备电源状态 D3 并保存上下文，但设备的驱动程序不得关闭设备电源。

如果系统 IRP 请求**PowerSystemShutdown**，则驱动程序应检查**IRP&gt;** 的 power\_操作值，然后才能确定状态更改的原因。 有关详细信息，请参阅[系统电源操作](system-power-actions.md)。

设备电源策略所有者必须为每个系统设置-电源 IRP 发送设备电源 IRP，即使设备已处于正确的设备电源状态。 如果驱动程序先前已将设备操作挂起，以响应查询-power IRP，则设置电源 IRP 会通知它停止对 Irp 的排队并返回到其当前电源状态的正常操作。 当设备处于 D3 状态时，将发生唯一的异常;在这种情况下，驱动程序不需要发送额外的[**IRP\_MN\_设置 D3\_POWER**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power) request。

 

 




