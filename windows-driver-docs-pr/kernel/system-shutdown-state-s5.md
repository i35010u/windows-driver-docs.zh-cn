---
title: 系统关闭状态 S5
description: 系统关闭状态 S5
ms.assetid: c08d688d-c31a-4d57-a343-406edfa35e8f
keywords:
- S5 WDK 电源管理
- 系统关闭状态 WDK 电源管理
- 软件恢复 WDK 电源管理
- 恢复 WDK 电源管理
- 硬件延迟 WDK 电源管理
- 系统硬件上下文 WDK 电源管理
- 硬件上下文 WDK 电源管理
- 上下文 WDK 电源管理
- 延迟 WDK 电源管理
- 系统电源状态 WDK 内核，关闭状态
- 关闭状态 WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c9df301c371a885e03170409c80cd05c1f63d8be
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345410"
---
# <a name="system-shutdown-state-s5"></a>系统关闭状态 S5





在 S5 或关闭状态下，计算机没有内存状态，而且不执行任何计算的任务。

状态 S4 和 S5 之间唯一的区别是，可以重新启动计算机从休眠文件中状态 S4，而从状态 S5 重新启动要求重新启动系统。

状态 S5 具有以下特征：

<a href="" id="power-consumption"></a>**功率消耗**  
关闭除渗透设备，例如电源按钮的当前。

<a href="" id="software-resumption"></a>**软件恢复**  
在唤醒时需要启动。

<a href="" id="hardware-latency"></a>**硬件延迟**  
长和未定义。 仅物理交互，例如用户按 ON 开关将使系统回到工作状态。 如果系统已进行了配置，可以还从恢复计时器唤醒 BIOS。

<a href="" id="system-hardware-context"></a>**系统硬件上下文**  
无保留。

 

 




