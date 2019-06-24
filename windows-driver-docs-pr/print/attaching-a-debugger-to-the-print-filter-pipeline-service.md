---
title: 将调试器附加到打印筛选器管道服务
description: 将调试器附加到打印筛选器管道服务
ms.assetid: d2e032f8-bdce-415a-8cf4-d9816b7c9de5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 93f632312ddd5a85fa8f1c8620d2224b4333172c
ms.sourcegitcommit: 5decd841b9fcd9f4245c96ee0c028894c1e19f94
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/22/2019
ms.locfileid: "67325928"
---
# <a name="attaching-a-debugger-to-the-print-filter-pipeline-service"></a>将调试器附加到打印筛选器管道服务


XPSDrv 驱动程序筛选器承载的打印筛选器管道服务 (printfilterpipelinesvc.exe)。 如果你想要将 Microsoft Windows 调试器 (WinDbg) 附加到的打印筛选器管道服务，有两种基本方式来执行此操作：

1.  使用 WinDbg 从命令行启动进程。

2.  将 WinDbg 附加到现有进程。

筛选器管道宿主必须启动打印后台处理程序，因此必须使用第二个选项来将 WinDbg 附加到进程。 但是，筛选器管道宿主可能不是永久性的。 该服务的新实例启动时的应用程序提交到打印队列的作业和作业已完成后不久终止服务。 它可能很难将 WinDbg 附加到 printfilterpipelinesvc.exe，提交打印作业之后，但之前你尝试调试的筛选器开始运行，尤其是如果你想要调试的筛选器启动或初始化代码。

若要解决此问题，可以修改量该 printfilterpipelinesvc.exe 仍然打印作业完成后存在的时间。 值由控制**PipelineHostTimeout**值的 HKEY\_本地\_机\\系统\\CurrentControlSet\\控件\\打印的注册表项。

使用以下步骤更改筛选器管道服务超时值：

1.  运行 Microsoft 注册表编辑器 (RegEdit) 并导航到 HKEY\_本地\_MACHINE\\系统\\CurrentControlSet\\控制\\打印。

2.  添加**PipelineHostTimeout** REG\_DWORD 注册表项，如果尚未存在的值。

3.  设置**PipelineHostTimeout**为超时值，以毫秒为单位。 设置一个足够大的值为自己提供充足的时间要附加的进程，并且已设置断点。 例如，如果你想 1.5 分钟的超时值，则设置**PipelineHostTimeout**到 90000。

设置后**PipelineHostTimeout**值时，请使用以下过程将 WinDbg 附加到管道筛选器服务：

1.  运行具有提升的权限的 WinDbg，但不是将其附加到进程。

2.  提交您的驱动程序的打印作业并等待其完成。 筛选器管道服务将继续运行指定的超时值。

3.  从 WinDbg 文件菜单中，选择附加到进程。

4.  在附加到进程对话框中，选择 printfilterpipelinesvc.exe 并单击确定。 如果进程被列为"拒绝访问"，这可能意味着 WinDbg 不使用提升的权限运行。

5.  根据需要设置断点。

6.  重新提交打印作业。

筛选器宿主进程应在第一个断点处调试器中中断或停止的第一个验证程序，具体取决于第一个。 在这里，可以单步执行代码、 检查变量和其他操作。

 

 




