---
title: 系统关闭状态 S5
description: 系统关闭状态 S5
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
ms.openlocfilehash: e38ff68adaba3eb39e28765242263887b713c68e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96841215"
---
# <a name="system-shutdown-state-s5"></a>系统关闭状态 S5





在 S5 或关闭状态下，计算机没有内存状态，并且不执行任何计算任务。

状态 S4 和 S5 之间唯一的区别在于，计算机可以从状态 S4 中的休眠文件重新启动，而从类型 S5 重新启动时，需要重新启动系统。

状态 S5 具有以下特征：

<a href="" id="power-consumption"></a>功率消耗  
关闭，除非滴为设备（如电源按钮）。

<a href="" id="software-resumption"></a>软件恢复  
需要在唤醒上启动。

<a href="" id="hardware-latency"></a>硬件延迟  
较长且不确定。 只有物理交互（如用户按下的开关）将系统恢复到工作状态。 如果系统已配置，则 BIOS 还可以从恢复计时器唤醒。

<a href="" id="system-hardware-context"></a>系统硬件上下文  
不保留任何内容。

 

 




