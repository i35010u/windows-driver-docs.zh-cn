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
ms.date: 07/30/2020
ms.localizationpriority: High
ms.openlocfilehash: 22f381fa1f43cf76ffff4f4d5c34f5e1ca266b7c
ms.sourcegitcommit: d1837118dd35d3b93eb9fb0f82a08c3340ff0ed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/14/2020
ms.locfileid: "92021031"
---
# <a name="system-sleeping-states"></a>系统睡眠状态





状态 S1、S2、S3 和 S4 为睡眠状态。 处于这些状态之一的系统不执行任何计算任务，似乎处于关闭状态。 但是，与处于关机状态 (S5) 的系统不同，处于休眠状态的系统会在 RAM 或磁盘上保留内存状态，如“系统硬件上下文”部分中为以下每种电源状态所指定的那样。 操作系统无需重新启动即可将计算机恢复到工作状态。

某些设备可在发生某些事件时将系统从睡眠状态唤醒。 此外，在某些计算机上，外部指示器会告诉用户系统只是处于睡眠状态。

每个连续的睡眠状态按照从 S1 到 S4 的顺序，会关闭计算机的更多功能。 所有 ACPI 兼容的计算机都会在 S1 时关闭处理器时钟，并在 S4 时丢失系统硬件上下文（除非在关机前写入休眠文件），如以下部分所示。

中间睡眠状态的详细信息可能因制造商设计计算机的方式不同而异。 例如，在某些计算机上，主板上的某些芯片可能会在 S3 时断电，而其他一些芯片会保持电源，直到进入 S4 状态。 此外，某些设备只能从 S1 唤醒系统，而不能从更深的睡眠状态唤醒系统。

使用 `powercfg /a` 枚举系统上的所有可用睡眠状态。 用户可使用[睡眠按钮操作](/windows-hardware/customize/power-settings/power-button-and-lid-settings-sleep-button-action)，指定在按下“睡眠”电源按钮时要执行的操作。

通常，在用户按睡眠按钮后，系统将进入系统电源状态 S3。

若要限制系统，使其只能进入部分 Sx 状态，用户可在 https://docs.microsoft.com/windows/win32/api/winnt/ns-winnt-system_power_policy （和 https://docs.microsoft.com/windows/win32/api/winnt/ns-winnt-administrator_power_policy) ）中提供“最长睡眠时间”和“最短睡眠时间”字段**p** 。 

### <a name="system-power-state-s1"></a>系统电源状态 S1

系统电源状态 S1 为睡眠状态，具有以下特征：

<a href="" id="power-consumption"></a>功率消耗  
消耗比 S0 少，但比其他睡眠状态多。 处理器时钟已关闭，并且停止了总线时钟。

<a href="" id="software-resumption"></a>软件恢复  
控件从中断位置重启。

<a href="" id="hardware-latency"></a>硬件延迟  
通常不超过两秒。

<a href="" id="system-hardware-context"></a>系统硬件上下文  
硬件保留并维护所有上下文。

### <a name="system-power-state-s2"></a>系统电源状态 S2

系统电源状态 S2 与 S1 类似，只是由于处理器断电，CPU 上下文和系统缓存的内容将丢失。 状态 S2 具有以下特征：

<a href="" id="power-consumption"></a>功率消耗  
消耗小于状态 S1，大于 S3。 处理器关闭。 总线时钟停止，某些总线可能会断电。

<a href="" id="software-resumption"></a>软件恢复  
唤醒后，控件从处理器的重置向量启动。

<a href="" id="hardware-latency"></a>硬件延迟  
两秒钟或更长时间，大于或等于 S1 的延迟。

<a href="" id="system-hardware-context"></a>系统硬件上下文  
CPU 上下文和系统缓存内容丢失。

### <a name="system-power-state-s3"></a>系统电源状态 S3

系统电源状态 S3 为睡眠状态，其特征如下：

<a href="" id="power-consumption"></a>功率消耗  
消耗小于状态 S2。 处理器已关闭，并且主板上的一些芯片也可能已关闭。

<a href="" id="software-resumption"></a>软件恢复  
出现唤醒事件后，控件从处理器的重置向量启动。

<a href="" id="hardware-latency"></a>硬件延迟  
与 S2 相当。

<a href="" id="system-hardware-context"></a>系统硬件上下文  
仅保留系统内存。 CPU 上下文、缓存内容和芯片组上下文都将丢失。

### <a name="system-power-state-s4"></a>系统电源状态 S4

系统电源状态 S4（休眠状态）是耗电最低且唤醒延迟最长的睡眠状态。 为了将能耗降到最低，硬件会关闭所有设备。 但是，操作系统上下文会保留在系统在进入 S4 状态之前写入到磁盘的休眠文件（内存映像）中。 重启时，加载程序将读取此文件，并跳到系统以前的休眠前位置。

如果处于 S1、S2 或 S3 状态的计算机完全断电，则会丢失系统硬件上下文，因此必须重新启动才能返回到 S0。 但是，即使断电，也可以从以前的位置重启 S4 状态的计算机，因为在休眠文件中保留了操作系统上下文。 处于休眠状态的计算机不使用任何电源（涓流电流除外）。

状态 S4 具有以下特征：

<a href="" id="power-consumption"></a>功率消耗  
关闭，电源按钮和类似设备上的涓流电流除外。

<a href="" id="software-resumption"></a>软件恢复  
系统从保存的休眠文件重启。 如果无法加载休眠文件，则需要重新启动。 当系统处于 S4 状态时重新配置硬件可能会产生更改，导致无法正确加载休眠文件。

<a href="" id="hardware-latency"></a>硬件延迟  
较长且不确定。 只能通过物理交互将系统恢复到工作状态。 此类交互可能包括用户按下启动开关，或者调制解调器上的来电响铃或 LAN 上出现活动（如果存在相应的硬件并启用了唤醒）。 如果硬件支持，计算机还可以从恢复计时器唤醒。

<a href="" id="system-hardware-context"></a>系统硬件上下文  
硬件中没有保留。 系统在关机之前，将内存映像写入休眠文件。 加载操作系统后，它将读取此文件并跳转到其之前的位置。

 

