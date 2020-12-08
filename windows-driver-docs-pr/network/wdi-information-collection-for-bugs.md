---
title: WDI 信息收集 bug
description: 任何不重要的软件中的 bug 都是不可避免的。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c303a91456c5ab16a6adf696f6630fb0f89183ef
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825385"
---
# <a name="wdi-information-collection-for-bugs"></a>WDI 信息收集 bug


任何不重要的软件中的 bug 都是不可避免的。 在驱动程序开发阶段，bug 和调试活动应为工作的一个不重要部分。 Bug 可能需要公司内工作，因为它们可以在操作系统、WDI UE 或 WDI LE 中。 收集相关信息以快速缩小根本原因，这一点非常重要。 收集的信息因错误性质而异。 有时需要重复重现 bug 的重现以收集进一步的信息，但这对于尽可能多地减少迭代至关重要。 下面是一些从开始的规则。

## <a name="os-crash-without-kernel-debugger-attached"></a>未连接内核调试器的操作系统崩溃


操作系统生成故障转储。 有不同类型的故障转储，如微型转储和完全转储。 虽然小型转储非常小，但通常仅适用于会审。 为了根本引起问题，几乎总是需要完全转储。 建议在驱动程序开发和自承载阶段启用完全转储。 启用完全转储：

1.  在桌面上右键单击 **此电脑** ，然后选择 " **属性**"。
2.  在 " **高级** " 选项卡上，打开 " **启动和恢复** " 部分，然后单击 " **设置 ...** " 按钮。
3.  在 " **写入调试信息** " 部分中，选择 " **内核内存转储** " (，而不是) 的 " **自动内存转储** "。

当操作系统发生崩溃时，将在% windir% 内存 dmp 生成内存转储文件 \\ 。
## <a name="os-crash-with-kernel-debugger-attached"></a>连接内核调试器时出现操作系统崩溃


如果可能，开发人员或 QA 应连接内核调试。 内核调试器可以快速判断出错误的原因以及要进一步调查的方向。 Kd 命令 "[**！分析**](../debugger/-analyze.md) – v" 可用作 bug 检查后运行的第一个命令。 此命令指向某个模块内发生崩溃的位置，以及导致崩溃 (bug 检查代码) 的位置。

## <a name="when-reset-recovery-is-invoked"></a>调用重置恢复时


如果调用重置恢复，WDI 的重置恢复功能将生成收集实时内核转储的能力。 内核转储使开发人员能够调查根本原因事后的根本原因。 实时内核转储在% windir% LiveKernelDumps 下收集 \\ 。

### <a name="reset-recovery-triggers"></a>重置恢复触发器

下面列出了当前的重置恢复触发器。 将来可能会添加更多触发器。

-   UE) 发送到 LE (M3 检测到 WDI 命令超时。
-   UE) 发送到 LE (的 M4 检测到 WDI 任务的超时。
-   该 LE 检测并指示固件挂起。
-   用户模式请求重置恢复。 此情况目前仅用于丢失 internet 连接。 如果 NIC 已连接并且具有 internet 连接，wlansvc 将启动 internet 丢失状态机。 如果 internet 连接丢失且在35秒内未重新获得，wlansvc 将请求 WDI 启动重置恢复。 35秒超时可能会在将来发生变化。

### <a name="events-for-reset-recovery-triggers"></a>重置恢复触发器的事件

WDI 调用 NDIS 将错误事件记录到系统事件日志（在收到重置恢复触发器时）。 事件在 LE 名称中，ID 为5002。 最后两个 Dword 为 \[ TriggerType、ActiveWdiCommand \] 。 下面列出了当前的触发器类型。

-   命令 \_ 计时器已 \_ 运行 (1) 
-   任务 \_ 计时器已 \_ 用 (2) 
-   重置 \_ 恢复 \_ OID \_ 请求 (3) 
-   重置 \_ 恢复 \_ 固件 \_ 停止 (4) 

如果触发器类型为 RESET \_ 恢复 \_ OID \_ 请求或重置 \_ 恢复 \_ 固件 \_ 停止，ActiveWdiCommand 可能为 0 (没有活动的命令) 。

此屏幕截图是显示系统 .evtx 的 eventvwr.msc 的一个示例视图。 触发器类型为3，并且没有活动的命令。

![wdi 事件日志屏幕快照](images/wdi-event-log-screenshot.png)

## <a name="when-wi-fi-malfunctions"></a>Wi-Fi 故障时


如果没有崩溃但 Wi-Fi 未按预期运行，请收集和分析跟踪日志。 若要查看问题是否局限于 WDI UE and LE， \_ 应包含 wlan dbg 跟踪来查看上下文的操作系统事件。 Wlan \_ dbg 包含需要操作系统专用符号的 WPP 事件。 原始 etl 跟踪应该保留并包含在通信中。

## <a name="connected-standby-issues"></a>连接待机问题


有时，Wi-Fi NIC 不会转向低功耗 (设备 \_ 电源 \_ 状态 \_ Dx) 。 其他情况下，设备会频繁唤醒。 SleepStudy 报表有助于第一级会审。 SleepStudy 事件始终为 on，但仅当 CS 会话超过10分钟时才收集。 这些事件也是持久性 (例如，您可以检查研究总结) 。 若要生成 SleepStudy，请在管理员命令提示符下运行以下命令行。

```CMD
Powercfg /SleepStudy
```

生成名为 SleepStudy-report.html 的报告文件。 它应该在% windiir% 系统之外打开 \\ 。 该报告分解哪些模块将系统的电源状态降低为非常低， (DRIPS) 。 此外，它还可以进一步细分哪些组件将 Wi-Fi NIC 保持 () Dx。

 

