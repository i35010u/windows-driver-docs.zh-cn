---
title: 将调试器附加到打印筛选器管道服务
description: 将调试器附加到打印筛选器管道服务
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c4a875bf79f150d3b1fe201033854b43bff67fd0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836125"
---
# <a name="attaching-a-debugger-to-the-print-filter-pipeline-service"></a>将调试器附加到打印筛选器管道服务


XPSDrv 驱动程序筛选器由打印筛选器管道服务承载 ( # A0) 。 如果要将 Microsoft Windows 调试器 (WinDbg) 附加到打印筛选器管道服务，可通过两种基本方式执行此操作：

1.  在命令行中使用 WinDbg 启动该过程。

2.  将 WinDbg 附加到现有进程。

筛选器管道主机必须由打印后台处理程序启动，因此您必须使用第二个选项将 WinDbg 附加到该进程。 但是，筛选器管道主机可能不是永久性的。 当应用程序将作业提交到打印队列时，会启动服务的新实例，并在作业完成之后不久终止该服务。 在提交打印作业之后但在尝试调试的筛选器开始运行之前，可能很难将 WinDbg 附加到 printfilterpipelinesvc.exe 中，特别是在您想要调试筛选器的启动或初始化代码时。

若要解决此问题，可以修改打印作业完成后 printfilterpipelinesvc.exe 保持的时间。 该值由 HKEY **PipelineHostTimeout** \_ 本地 \_ 计算机 \\ 系统 \\ CurrentControlSet 控件 "打印" \\ \\ 注册表项的 PipelineHostTimeout 值控制。

使用以下步骤可更改筛选器管道服务超时值：

1.   (RegEdit) 运行 Microsoft 注册表编辑器，然后导航到 "HKEY" "本地计算机" "CurrentControlSet" " \_ \_ 控制" \\ \\ \\ \\ 。

2.  **PipelineHostTimeout** \_ 如果键不存在，请向该项添加 PipelineHostTimeout 注册表 DWORD 值。

3.  将 **PipelineHostTimeout** 设置为超时值（以毫秒为单位）。 设置足够大的值，以使自己有充足的时间来附加进程并设置断点。 例如，如果要将超时值设置为1.5 分钟，请将 **PipelineHostTimeout** 设置为90000。

设置 **PipelineHostTimeout** 值后，请使用以下过程将 WinDbg 附加到管道筛选器服务：

1.  使用提升的权限运行 WinDbg，但不要将其附加到进程。

2.  将打印作业提交到您的驱动程序并等待其完成。 筛选器管道服务将继续运行指定的超时值。

3.  从 "WinDbg 文件" 菜单中，选择 "附加到进程"。

4.  在 "附加到进程" 对话框中，选择 printfilterpipelinesvc.exe 然后单击 "确定"。 如果该进程列出为 "拒绝访问"，则很可能意味着 WinDbg 未使用提升的权限运行。

5.  根据需要设置断点。

6.  再次提交打印作业。

筛选器宿主进程应在第一个断点处中断调试器，或在第一个验证程序停止时中断，以先执行的操作为准。 在这里，你可以单步执行代码、检查变量等。

 

 




