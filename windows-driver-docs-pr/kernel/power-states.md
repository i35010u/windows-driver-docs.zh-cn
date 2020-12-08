---
title: 电源状态
description: 电源状态
keywords:
- 电源管理 WDK 内核，电源状态
- 电源状态 WDK 内核
- 状态 WDK 电源管理
- 系统电源状态 WDK 内核
- 设备电源状态 WDK 内核
- 能源消耗级别 WDK 内核
- 消耗级别 WDK 电源管理
- 计算活动 WDK 电源管理
- 物理设备对象 WDK 电源管理
- PDO WDK 电源管理
- 功能设备对象 WDK 电源管理
- FDOs WDK 电源管理
- 筛选器 DO WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b6387cf2f5606bf02db6afe64c563fc3f42a61fb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836913"
---
# <a name="power-states"></a>电源状态





电源状态指示系统或单个设备的电源消耗级别，进而指示计算活动的范围。 Power manager 将系统的电源状态设置为整体。 设备驱动程序设置各自设备的电源状态。

ACPI 规范定义了两个不同的电源状态集： *系统电源状态* 和 *设备电源* 状态。 每个电源状态都具有唯一的名称。

[系统电源状态](system-power-states.md) 名为 S *x*，其中 *x* 是介于0和5之间的状态。 [设备电源状态](device-power-states.md) 的名称为 D *x*，其中 *x* 是介于0到3之间的状态。 状态号码与功率消耗成反比：更高编号的状态使用更少的电量。 状态 S0 和 D0 是最高性能、功能最高、功能完全可用的状态。 状态 S5 和 D3 是最低的驱动状态，并且具有最长的唤醒延迟。

这些清晰定义的电源状态允许各种制造商提供的多个设备以一致且可预测的方式协同工作。 例如，当 power manager 将系统设置为 S3 时，它可以依赖于支持电源管理的驱动程序，不仅可以将设备置于相应的设备电源状态，还可以以可预测的方式返回到工作状态。

 

 




