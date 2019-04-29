---
title: 电源状态
description: 电源状态
ms.assetid: 33043903-9db6-4c51-b33c-921ade237ccf
keywords:
- 电源管理 WDK 内核，电源状态
- 电源状态 WDK 内核
- 指出 WDK 电源管理
- 系统电源状态 WDK 内核
- 设备电源状态 WDK 内核
- 电源消耗级别 WDK 内核
- 消耗级别 WDK 电源管理
- 计算活动 WDK 电源管理
- 物理设备对象 WDK 电源管理
- PDOs WDK 电源管理
- 功能的设备对象 WDK 电源管理
- FDOs WDK 电源管理
- 筛选器 DOs WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 99cedd1ffa93ac477d83ac33953202c6dd2c24f4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369147"
---
# <a name="power-states"></a>电源状态





电源状态指示的功率消耗级别 — 因此计算活动的范围 — 由系统或通过单个设备。 电源管理器作为一个整体设置系统电源的状态。 设备驱动程序设置其每个设备的电源状态。

ACPI 规范定义了离散的电源状态的两个集：*系统的电源状态*并*设备的电源状态*。 每个电源状态具有唯一的名称。

[系统电源状态](system-power-states.md)名为 S*x*，其中*x*是介于 0 和 5 之间的状态。 [设备的电源状态](device-power-states.md)名为 D*x*，其中*x*是介于 0 和 3 之间的状态。 状态数成反比与功率消耗： 更高版本带编号的状态使用较少的电量。 状态 S0 和 D0 是 highest-powered 最上正常运行，完全状态。 状态 S5 和 D3 进行的最低支持的状态，并将最长唤醒延迟。

这些明确定义的电源状态允许来自各个制造商以一致、 可以预见协同工作的多个设备。 例如，当电源管理器状态 S3 中设置的系统，它可以依赖于支持电源管理以将其设备放入相应的设备电源状态不仅还可以返回到以可预测的方式工作的状态的驱动程序。

 

 




