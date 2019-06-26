---
title: 确定正确的设备电源状态
description: 确定正确的设备电源状态
ms.assetid: 4acefe93-1d7a-4c12-8701-03c2a8929591
keywords:
- DEVICE_CAPABILITIES 结构
- 正确的设备的电源状态 WDK 电源管理
- 设备电源状态 WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6d52a4beea6eb55f1e75bdc37fa76a8f127d804c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371272"
---
# <a name="determining-the-correct-device-power-state"></a>确定正确的设备电源状态





电源策略所有者检查[ **DeviceState** ](devicestate.md)数组中[**设备\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_capabilities)结构，以确定为每个系统电源状态的设备的电源状态的有效范围。 该数组列出了基础设备可以支持为每个系统电源状态的最高设备电源状态。

在此范围从选择某一特定状态时，考虑以下方面：

-   当系统进入 S0 状态时，大多数设备输入 D0 状态。

-   当系统进入任何睡眠状态时，大多数设备输入 D3 状态。 但是，启用了唤醒的设备可能需要输入 D1 或 D2 相反，如果支持这种状态。 有关详细信息，请参阅[报告设备电源功能](reporting-device-power-capabilities.md)。

-   特殊规则也适用于将保存休眠文件的设备。 如果请求系统 IRP **PowerSystemHibernate**，将保存休眠文件的设备必须不关闭电源。 此类设备的电源策略所有者应请求设备电源状态 D3 和保存上下文，但设备的驱动程序必须关闭设备电源。

如果系统 IRP 请求**PowerSystemShutdown**，该驱动程序应检查电源\_处的操作值**Irp-&gt;Parameters.Power.ShutdownType**以确定原因状态更改。 有关详细信息，请参阅[系统电源操作](system-power-actions.md)。

设备电源策略所有者必须将设备发送的每个系统集 power IRP 集 power IRP，即使设备已处于正确的设备电源状态。 如果该驱动程序先前挂起设备操作，以响应查询能耗 IRP，集 power IRP 通知它停止队列 Irp 并返回到其当前的电源状态的正常操作。 当设备处于 D3 状态，则唯一的例外时发生在这种情况下，驱动程序需要不发送额外[ **IRP\_MN\_设置\_POWER** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power) D3 的请求。

 

 




