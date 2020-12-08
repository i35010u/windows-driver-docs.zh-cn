---
title: 调试 XPSDrv 打印机驱动程序
description: 调试 XPSDrv 打印机驱动程序
keywords:
- 调试 XPSDrv 驱动程序 WDK 打印
- XPSDrv 驱动程序调试 WDK 打印
- XPSDrv 打印机驱动程序 WDK，调试
- spoolsv.exe 处理 WDK 打印
- printfilterpipelinesvc.exe 处理 WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7e2338ef2a0bf49005868a96802204268cc096f9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797325"
---
# <a name="debugging-xpsdrv-printer-drivers"></a>调试 XPSDrv 打印机驱动程序


包含 XPSDrv 打印机驱动程序的打印队列在 spoolsv.exe 过程中托管。 但是，与基于 GDI 的打印机驱动程序不同的是，XPSDrv 打印机驱动程序的筛选器承载在 printfilterpipelinesvc.exe 过程中，该进程与 spoolsv.exe 分离。 因此，必须将调试器附加到 printfilterpipelinesvc.exe 进程，才能在 XPSDrv 打印机驱动程序中调试筛选器。

### <a name="configuring-the-printfilterpipelinesvcexe-process-time-out"></a><a href="" id="configuring-the-printfilterpipelinesvc-exe-process-time-out"></a>配置 printfilterpipelinesvc.exe 进程 Time-Out

当使用 XPSDrv 打印机驱动程序将打印作业发送到打印队列时，printfilterpipelinesvc.exe 进程开始。 此过程在注册表中由值定义的一段时间内处于非活动状态后退出。 printfilterpipelinesvc.exe 进程的间歇特性使得将调试器附加到 printfilterpipelinesvc.exe 很难在 XPSDriv 打印机驱动程序中调试筛选器。

但是，你可以在注册表中配置非活动超时期限。 注册表中 " **HKEY \_ 本地 \_ 计算机 \\ 系统 \\ CurrentControlSet 控件" \\ \\ 输出** 子项下的 PipelineHostTimeout 值定义 printfilterpipelinesvc.exe 进程超时（以毫秒为单位）。 可以增大此值，以便更轻松地调试 XPSDrv 打印机驱动程序。 请注意，printfilterpipelinesvc.exe 进程开始分析配置文件，以便即使没有为驱动程序定义任何筛选器，该进程仍将启动。

### <a name="configuring-the-system-for-debugging"></a>配置系统以进行调试

若要调试 XPSDrv 打印机驱动程序，您必须：

1.  分配使用要调试的驱动程序的打印队列，打印到文件端口。

2.  将 PipelineHostTimeout 值设置为一个值，该值可用于调试问题。

3.  将打印作业发送到你在步骤1中创建的打印队列，以启动 Printfilterpipelinesvc.exe 进程。

4.  将调试器附加到 Printfilterpipelinesvc.exe 进程，然后开始调试。

附加调试器后，可以在筛选器模块中设置断点并开始调试打印机驱动程序。

如果要调试的打印机驱动程序导致 printfilterpipelinesvc.exe 进程在您可以附加调试器之前退出，则可以执行以下操作：

1.  创建不具有配置文件中定义的任何筛选器的 XPSDrv 打印机驱动程序。

2.  使用在上一步中创建的打印机驱动程序创建打印队列。

3.  分配使用要调试的驱动程序的打印队列，打印到文件端口。

4.  将 PipelineHostTimeout 值设置为一个值，该值可用于调试问题。

5.  将打印作业发送到你在步骤2中创建的打印队列。

6.  将调试器附加到 Printfilterpipelinesvc.exe 进程。

7.  在要调试的打印机驱动程序中设置断点。

8.  用要调试的驱动程序打印到打印队列。

 

 




