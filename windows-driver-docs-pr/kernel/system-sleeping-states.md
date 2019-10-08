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
- 系统硬件环境 WDK 电源管理
- 硬件上下文 WDK 电源管理
- 上下文 WDK 电源管理
- 延迟 WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: High
ms.openlocfilehash: 52144a68515e30a58a398ab593f0f1ff160d505a
ms.sourcegitcommit: c73954a5909ec8c7e189f77fd5813f2eb749687c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/07/2019
ms.locfileid: "72007651"
---
# <a name="system-sleeping-states"></a>系统睡眠状态





状态 S1、S2、S3 和 S4 为睡眠状态。 处于这些状态之一的系统不执行任何计算任务，似乎处于关闭状态。 但与关闭状态（S5）中的系统不同，睡眠系统会保留硬件或磁盘上的内存状态。 操作系统无需重新启动即可将计算机恢复到工作状态。

某些设备可以在发生某些事件时将系统从睡眠状态唤醒，如传入的调制解调器呼叫。 此外，在某些计算机上，外部指示器会告诉用户系统只是处于睡眠状态。

对于每个连续睡眠状态（从 S1 到 S4），会关闭更多计算机。 所有符合 ACPI 标准的计算机都会在 S1 上关闭处理器时钟，并在 S4 上丢失系统硬件上下文（除非在关闭前写入休眠文件），如以下部分所示。 中间睡眠状态的详细信息可能因制造商设计计算机的方式而有所不同。 例如，在某些计算机上，主板上的某些芯片可能会失去 S3 的电量，而其他一些芯片会保持电源到 S4。 此外，某些设备只能从 S1 唤醒系统，而不能从深度睡眠状态唤醒。

### <a name="system-power-state-s1"></a>系统电源状态 S1

系统电源状态 S1 为睡眠状态，具有以下特征：

<a href="" id="power-consumption"></a>**功率消耗**  
使用比在 S0 中更少的消耗，在其他睡眠状态中则更少。 处理器时钟已关闭，并且停止了总线时钟。

<a href="" id="software-resumption"></a>**软件恢复**  
控件从中断位置重新启动。

<a href="" id="hardware-latency"></a>**硬件延迟**  
通常不超过两秒。

<a href="" id="system-hardware-context"></a>**系统硬件上下文**  
硬件保留并维护的所有上下文。

### <a name="system-power-state-s2"></a>系统电源状态 S2

系统电源状态 S2 与 S1 类似，只是 CPU 上下文和系统缓存的内容丢失，因为处理器断电。 状态 S2 具有以下特征：

<a href="" id="power-consumption"></a>**功率消耗**  
消耗的消耗小于状态 S1，大于 S3。 处理器关闭。 总线时钟停止;某些总线可能会断电。

<a href="" id="software-resumption"></a>**软件恢复**  
唤醒后，控件从处理器的重置向量开始。

<a href="" id="hardware-latency"></a>**硬件延迟**  
两秒钟或更多;大于或等于 S1 的延迟。

<a href="" id="system-hardware-context"></a>**系统硬件上下文**  
CPU 上下文和系统缓存内容丢失。

### <a name="system-power-state-s3"></a>系统电源状态 S3

系统电源状态 S3 为睡眠状态，其特征如下：

<a href="" id="power-consumption"></a>**功率消耗**  
消耗的消耗小于状态 S2。 处理器已关闭，并且主板上的一些芯片也可能已关闭。

<a href="" id="software-resumption"></a>**软件恢复**  
唤醒事件完成后，控件从处理器的重置向量开始。

<a href="" id="hardware-latency"></a>**硬件延迟**  
几乎不能与 S2 区分开来。

<a href="" id="system-hardware-context"></a>**系统硬件上下文**  
仅保留系统内存。 CPU 上下文、缓存内容和芯片组上下文都将丢失。

### <a name="system-power-state-s4"></a>系统电源状态 S4

系统电源状态 S4 （休眠状态）是处于最低状态的休眠状态，并且具有最长的唤醒延迟。 若要将能耗降到最低，则硬件会关闭所有设备。 但是，操作系统上下文保留在系统将其写入到磁盘中的休眠文件（内存映像）中，然后进入 S4 状态。 重新启动时，加载程序将读取此文件，并跳到系统以前的 prehibernation 位置。

如果处于 S1、S2 或 S3 状态的计算机丢失了所有交流电源或电池电量，则会丢失系统硬件上下文，因此必须重新启动才能返回到 S0。 但是，即使在睡眠文件中保留了操作系统上下文，也可以从以前的位置重启计算机。 处于休眠状态的计算机不使用任何电源（可能是因为滴当前的情况除外）。

状态 S4 具有以下特征：

<a href="" id="power-consumption"></a>**功率消耗**  
关闭，"滴" 按钮和类似设备上的 "当前" 除外。

<a href="" id="software-resumption"></a>**软件恢复**  
系统从保存的休眠文件重新启动。 如果无法加载休眠文件，则需要重新启动。 当系统处于 S4 状态时重新配置硬件可能会导致更改，导致无法正确加载休眠文件。

<a href="" id="hardware-latency"></a>**硬件延迟**  
Long 和 undefined。 只有物理交互将系统恢复到工作状态。 此类交互可能包括用户按下的开关，或者，如果提供了相应的硬件并启用了唤醒，则可以在 LAN 上使用调制解调器或活动的传入环。 如果硬件支持，计算机还可以从恢复计时器唤醒。

<a href="" id="system-hardware-context"></a>**系统硬件上下文**  
硬件中没有保留的。 系统在关机之前，将内存中的内存写入休眠文件。 加载操作系统后，它将读取此文件并跳转到其之前的位置。

 

 




