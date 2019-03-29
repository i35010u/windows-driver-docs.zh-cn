---
title: 系统睡眠状态
description: 系统睡眠状态
ms.assetid: 2fd883b5-4e89-4ce9-b75a-b821348ac860
keywords:
- 系统电源状态 WDK 内核，睡眠状态
- 系统睡眠状态 WDK 电源管理
- 睡眠状态 WDK 电源管理
- S1 WDK 电源管理
- S2 WDK 电源管理
- S3 WDK 电源管理
- S4 WDK 电源管理
- 软件恢复 WDK 电源管理
- 恢复 WDK 电源管理
- 硬件延迟 WDK 电源管理
- 系统硬件上下文 WDK 电源管理
- 硬件上下文 WDK 电源管理
- 上下文 WDK 电源管理
- 延迟 WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8d2eacbc7bf6863884dabd6611105c631e615cd4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565096"
---
# <a name="system-sleeping-states"></a>系统睡眠状态





状态 S1、 S2、 S3 和 S4 休眠状态。 其中一种状态中的系统不执行任何计算的任务，并显示处于关闭状态。 但是，与处于关闭状态 (S5) 系统，处于睡眠状态的系统保留内存状态，在硬件或磁盘上。 操作系统不需要重新启动才能将计算机恢复到工作状态。

发生某些事件，如对调制解调器的传入呼叫时，某些设备可以唤醒从睡眠状态系统。 此外，对于某些计算机，外部指示器会告知系统只处于休眠状态的用户。

与每个连续的睡眠状态，从 S1 到 S4，多个计算机关闭的情况下。 所有符合 ACPI 的计算机关闭其处理器时钟在 S1 并放弃在 S4 系统硬件上下文 （除非在关闭之前写入休眠文件），如以下各节中列出。 具体取决于制造商专门在计算机而异的中间睡眠状态的详细信息。 例如，在某些计算机上特定芯片母板上的可能会丢失在 S3，power 而对其他该种芯片保留 power 直到 S4。 此外，某些设备可能能够将系统只能从 S1 而不是从更深层次的睡眠状态唤醒。

### <a name="system-power-state-s1"></a>系统电源状态 S1

系统电源状态 S1 是休眠状态，具有以下特征：

<a href="" id="power-consumption"></a>**功率消耗**  
更少消耗比在 S0 和大于其他睡眠状态。 处理器时钟处于关闭状态和总线时钟已停止。

<a href="" id="software-resumption"></a>**软件恢复**  
控制重新启动中断的位置。

<a href="" id="hardware-latency"></a>**硬件延迟**  
通常不超过两秒。

<a href="" id="system-hardware-context"></a>**系统硬件上下文**  
所有上下文保留和维护的硬件。

### <a name="system-power-state-s2"></a>系统电源状态 S2

系统电源状态 S2 类似于 S1 只是因为处理器中断电，CPU 上下文和系统缓存的内容都会丢失。 状态 S2 具有以下特征：

<a href="" id="power-consumption"></a>**功率消耗**  
更少消耗比状态 S1 和 S3 中大于。 处理器处于关闭状态。 总线时钟已停止;某些总线可能会丢失电源。

<a href="" id="software-resumption"></a>**软件恢复**  
之后唤醒，控制首先体现在处理器的重置向量。

<a href="" id="hardware-latency"></a>**硬件延迟**  
两秒或更多;大于或等于适用于 S1 的延迟。

<a href="" id="system-hardware-context"></a>**系统硬件上下文**  
CPU 上下文和系统缓存内容都将丢失。

### <a name="system-power-state-s3"></a>系统电源状态 S3

系统电源状态 S3 是休眠状态，具有以下特征：

<a href="" id="power-consumption"></a>**功率消耗**  
更少状态 S2 中的消耗比。 处理器处于关闭状态，因此在主板上的某些芯片也可能关闭。

<a href="" id="software-resumption"></a>**软件恢复**  
唤醒事件之后，控制首先体现在处理器的重置向量。

<a href="" id="hardware-latency"></a>**硬件延迟**  
几乎没有区别 S2。

<a href="" id="system-hardware-context"></a>**系统硬件上下文**  
只有系统内存将保留。 CPU 上下文、 缓存内容和芯片集上下文都将丢失。

### <a name="system-power-state-s4"></a>系统电源状态 S4

系统电源状态 S4 休眠状态中，是最低提供支持的睡眠状态，最长唤醒延迟。 若要减少到最少的功率消耗，硬件，则关闭所有设备。 操作系统上下文中，但是，系统将写入到的休眠文件 （图像的内存） 中维护之前进入 S4 状态的磁盘。 重新启动后，加载程序将读取此文件，并跳转到系统的以前的 prehibernation 位置。

如果在 S1、 S2 或 S3 状态中的计算机丢失了所有 AC 或电池电源，它都失去系统硬件上下文，并因此必须重新启动才能恢复为 S0。 在状态中的计算机 S4，但是，可以重新启动从以前的位置甚至后会丢失电池或 AC 电源，因为操作系统上下文保留休眠文件中。 处于休眠状态的计算机使用任何电源 （与缓慢执行当前的可能异常）。

状态 S4 具有以下特征：

<a href="" id="power-consumption"></a>**功率消耗**  
关闭除渗透的电源按钮和类似的设备的当前。

<a href="" id="software-resumption"></a>**软件恢复**  
从已保存的休眠文件重新启动系统。 如果不能加载休眠文件，重新启动的需要。 使休眠文件无法正确加载的更改可能会导致系统处于 S4 状态时，重新配置硬件。

<a href="" id="hardware-latency"></a>**硬件延迟**  
长和未定义。 仅物理交互返回系统的工作状态。 这种交互可能包括用户按 ON 开关或，如果存在合适的硬件，并且启用了唤醒，传入圆环的调制解调器或 LAN 上的活动。 如果硬件支持，可以还从恢复计时器唤醒计算机。

<a href="" id="system-hardware-context"></a>**系统硬件上下文**  
无保留在硬件中。 在系统下打开电源之前的内存的图像写入休眠文件中。 加载操作系统时，它将读取此文件并跳转到以前的位置。

 

 




