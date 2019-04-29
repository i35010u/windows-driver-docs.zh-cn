---
title: 调试 XPSDrv 打印机驱动程序
description: 调试 XPSDrv 打印机驱动程序
ms.assetid: 7193f007-de25-4b77-9133-9937b3d37db0
keywords:
- 调试 XPSDrv 驱动程序 WDK 打印
- XPSDrv 驱动程序调试 WDK 打印
- XPSDrv 的打印机驱动程序 WDK，调试
- spoolsv.exe 过程 WDK 打印
- printfilterpipelinesvc.exe 过程 WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 809e49f2afffe4ea4f77b2e78868f3b1515d7421
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384957"
---
# <a name="debugging-xpsdrv-printer-drivers"></a>调试 XPSDrv 打印机驱动程序


打印使用 XPSDrv 打印机驱动程序会在 spoolsv.exe 进程中承载的队列。 与不同的是基于 GDI 的打印机驱动程序，但是，XPSDrv 打印机驱动程序的筛选器是在进程中托管 printfilterpipelinesvc.exe，这不同于 spoolsv.exe。 因此，必须将调试器附加到要调试的 XPSDrv 打印机驱动程序中的筛选器的 printfilterpipelinesvc.exe 进程。

### <a href="" id="configuring-the-printfilterpipelinesvc-exe-process-time-out"></a>配置 printfilterpipelinesvc.exe 进程超时

Printfilterpipelinesvc.exe 过程开始打印作业发送到使用 XPSDrv 打印机驱动程序的打印队列时。 在处于非活动状态的注册表中的值来定义的时间段后，在进程退出。 Printfilterpipelinesvc.exe 过程是间歇性难以将调试器附加到 printfilterpipelinesvc.exe 调试 XPSDriv 打印机驱动程序中的筛选器。

但是，您可以在注册表中配置停止活动超时时间。 下的 PipelineHostTimeout 值**HKEY\_本地\_机\\系统\\CurrentControlSet\\控制\\打印**子项中注册表以毫秒为单位定义 printfilterpipelinesvc.exe 进程超时。 可以增大此值以使其更易于调试 XPSDrv 打印机驱动程序。 请注意 printfilterpipelinesvc.exe 进程启动用于分析配置文件，以便即使没有筛选器驱动程序的定义，将仍能启动进程。

### <a name="configuring-the-system-for-debugging"></a>配置系统以进行调试

若要调试的 XPSDrv 打印机驱动程序，您必须：

1.  分配使用你想要调试以打印到文件端口驱动的程序的打印队列。

2.  PipelineHostTimeout 值设置为一个值，将为您提供足够的时间来调试问题。

3.  步骤 1 以启动 Printfilterpipelinesvc.exe 过程中创建打印作业发送到打印队列。

4.  将调试器附加到 Printfilterpipelinesvc.exe 进程并开始调试。

已附加调试器后，可以在筛选器模块中设置断点并开始调试打印机驱动程序。

如果你想要调试的打印机驱动程序导致 printfilterpipelinesvc.exe 进程退出之前可以附加调试器，您可以执行以下操作：

1.  创建不具有配置文件中定义的任何筛选器的 XPSDrv 打印机驱动程序。

2.  使用在上一步中创建的打印机驱动程序创建的打印队列。

3.  分配使用你想要调试以打印到文件端口驱动的程序的打印队列。

4.  PipelineHostTimeout 值设置为一个值，将为您提供足够的时间来调试问题。

5.  将打印作业发送到在步骤 2 中创建的打印队列。

6.  将调试器附加到 Printfilterpipelinesvc.exe 进程。

7.  在你想要调试的打印机驱动程序中设置断点。

8.  打印到打印队列使用你想要调试的驱动程序。

 

 




