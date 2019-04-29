---
title: WDI 信息收集的 bug
description: 在任何重要的软件中的 bug 是不可避免的。
ms.assetid: 551CA7DD-EB1A-41FB-A3D7-472DA7020B51
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f211168ac1d9db1b3b3f236b6174e4a2cfc81e0e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63385443"
---
# <a name="wdi-information-collection-for-bugs"></a>WDI 信息收集的 bug


在任何重要的软件中的 bug 是不可避免的。 在驱动程序开发阶段，bug 和调试活动都将是这项工作的重要组成部分。 Bug 可能需要联合公司工作，因为它们可以是在操作系统、 WDI UE 或 WDI LE。 若要收集相关的信息来快速缩小根本原因至关重要。 若要收集的信息根据性质的 bug 的变化很大。 重现的 bug，因此可以收集更多的信息的迭代有时有必要，但很重要，以减少最大程度地这些迭代。 下面首先是一些规则。

## <a name="os-crash-without-kernel-debugger-attached"></a>而无需内核调试程序附加的 OS 崩溃


操作系统生成故障转储。 有不同类型的故障转储，如小型转储和完全转储。 微型转储很小，而是通常只适用于会审。 到了的问题的根本原因，顺序完全转储几乎始终是必需的。 建议在驱动程序开发期间启用完全转储和自承载阶段。 若要启用完全转储：

1.  从桌面上，右键单击**此电脑**，然后选择**属性**。
2.  上**高级**选项卡上，转到**启动和恢复**部分，并单击**设置...** 按钮。
3.  在中**写入调试信息**部分中，选择**内核内存转储**(而非**自动内存转储**)。

当操作系统崩溃发生时，在 %windir%处生成内存转储文件\\memory.dmp。
## <a name="os-crash-with-kernel-debugger-attached"></a>使用内核调试程序附加的 OS 崩溃


开发人员或 QA 应具有内核调试程序附加在可能的情况。 内核调试程序可以快速区分到底出在哪儿和方向进行进一步调查。 Kd 命令[**！ 分析**](https://msdn.microsoft.com/library/windows/hardware/ff562112) – v 作为第一个命令运行后的 bug 检查非常有用。 此命令将指向崩溃发生的模块，在发生崩溃的原因 （错误检查代码） 中的位置。

## <a name="when-reset-recovery-is-invoked"></a>调用重置恢复时


WDI 的重置恢复功能构建调用重置恢复时收集实时内核转储的功能。 核心转储使开发人员能够调查根本原因事后。 转储收集 %windir%下的实时内核\\LiveKernelDumps。

### <a name="reset-recovery-triggers"></a>重置恢复触发器

下面列出了当前的重置恢复触发器。 可能在将来添加更多触发器。

-   UE 检测到 WDI 命令 (M3) 发送到 LE 的超时。
-   UE 检测到 WDI 任务 (M4) 发送到 LE 的超时。
-   LE 检测，并指示固件挂起。
-   用户模式下请求重置恢复。 这是当前仅为 internet 连接丢失。 当 NIC 连接并且已建立 internet 连接时，wlansvc 启动 internet 丢失状态机。 如果 internet 连接丢失，重新在 35 秒内未获得 wlansvc 请求 WDI 开始重置恢复。 35 秒超时将来会发生变化。

### <a name="events-for-reset-recovery-triggers"></a>重置恢复触发器的事件

WDI 调用 NDIS 接收重置恢复触发器时到系统事件日志中记录错误事件。 该事件处于 LE 名称，该 ID 是 5002。 最后两个 dword 值是\[TriggerType、 ActiveWdiCommand\]。 下面列出了当前的触发器类型。

-   命令\_计时器\_运行 (1)
-   任务\_计时器\_已用 (2)
-   重置\_恢复\_OID\_请求 (3)
-   重置\_恢复\_固件\_STALLED (4)

ActiveWdiCommand 可能为 0 （无活动命令），如果触发器类型重置\_恢复\_OID\_请求或重置\_恢复\_固件\_STALLED。

这是屏幕截图显示 system.evtx eventvwr 示例视图。 触发器类型为 3，并且没有任何活动命令。

![wdi 事件日志的屏幕截图](images/wdi-event-log-screenshot.png)

## <a name="when-wi-fi-malfunctions"></a>当 Wi-fi 工作不正常


如果没有任何故障，但 Wi-fi 不无法按预期运行，收集和分析跟踪日志。 若要查看此问题仅限于 WDI UE 和 LE，wlan\_dbg 跟踪应包括在内，以查看上下文的操作系统事件。 Wlan\_dbg 包含需要操作系统私有符号的 WPP 事件。 应保留原始 etl 跟踪，并将其包含在通信。

## <a name="connected-standby-issues"></a>连接待机状态问题


有时，Wi-fi NIC 不会为低能耗 (设备\_电源\_状态\_Dx)。 其他情况下，设备被唤醒频繁。 SleepStudy 报表是在第一个级别会审中有所帮助。 SleepStudy 事件将始终启用，但如果 CS 会话时间超过 10 分钟，才收集。 事件也是持久性 （例如，您可以检查研究总结）。 若要生成 SleepStudy，在管理员命令提示符中运行以下命令行。

```CMD
Powercfg /SleepStudy
```

生成一个名为 SleepStudy report.html 的报表文件。 它应打开外部 %windiir%\\系统。 报表会详细列出哪些模块保持系统的带非常低功耗状态 (DRIPS)。 它还可以进一步可以分解的组件够 Wi-fi NIC （带 Dx)。

 

 





