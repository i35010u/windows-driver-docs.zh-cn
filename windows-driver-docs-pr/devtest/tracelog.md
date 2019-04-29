---
title: Tracelog
description: 跟踪日志 (Tracelog.exe) 是在命令提示符窗口中运行的事件跟踪控制器。 本部分介绍 Tracelog，说明了其命令语法，并供其使用提供实际示例。
ms.assetid: aa3c144d-260b-44d2-b41c-d18be40ba541
keywords:
- Tracelog WDK
- 软件跟踪 WDK，跟踪日志
- 跟踪 WDK，跟踪日志
- 事件跟踪控制器 WDK Tracelog
- 跟踪会话管理 WDK Tracelog
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d1505480232f53ad163fb5204c5d0375a8e0f0ee
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369717"
---
# <a name="tracelog"></a>Tracelog


跟踪日志 (Tracelog.exe) 是在命令提示符窗口中运行的事件跟踪控制器。 本部分介绍 Tracelog，说明了其命令语法，并供其使用提供实际示例。

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">哪里可以获得 Tracelog？</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>在安装 WDK、 Visual Studio 和适用于桌面应用程序的 Windows SDK 时，Tracelog (Tracelog.exe) 是包含。 有关下载工具包的信息，请参阅<a href="https://go.microsoft.com/fwlink/p/?linkid=290798" data-raw-source="[Windows Hardware Downloads](https://go.microsoft.com/fwlink/p/?linkid=290798)">下载 Windows 硬件</a>。</p>
<p><strong>Windows Driver Kit (WDK) 8</strong> （安装路径）</p>
<p>%WindowsSdkDir%\tools\x64\tracelog.exe</p>
<p>%WindowsSdkDir%\tools\x86\tracelog.exe</p>
<p><strong>Windows Driver Kit (WDK) 8.1</strong> （安装路径）</p>
<p>%WindowsSdkDir%\bin\x64\tracelog.exe</p>
<p>%WindowsSdkDir%\bin\x86\tracelog.exe</p>
<div class="alert">
<strong>请注意</strong>  Visual Studio 环境变量，%windowssdkdir%，表示 Windows 工具包工具包安装的目录，例如，C:\Program Files (x86) \Windows Kits\8.1 的路径。
</div>
</td>
</tr>
</tbody>
</table>

 

## <a name="span-idwhatyoucandowithtracelogspanspan-idwhatyoucandowithtracelogspanspan-idwhatyoucandowithtracelogspanwhat-you-can-do-with-tracelog"></a><span id="What_you_can_do_with_Tracelog"></span><span id="what_you_can_do_with_tracelog"></span><span id="WHAT_YOU_CAN_DO_WITH_TRACELOG"></span>对跟踪日志可以执行哪些操作


可以在命令提示符窗口中使用跟踪日志，作为事件跟踪控制器。

**请注意**  来控制跟踪会话必须是 Performance Log Users 组或计算机上的管理员组的成员 (**以管理员身份运行**)。

Tracelog 功能包括：

-   启动和停止[跟踪会话](trace-session.md)，包括专用跟踪会话[NT 内核记录器跟踪会话](nt-kernel-logger-trace-session.md)，和[全局记录器跟踪会话](global-logger-trace-session.md)

-   配置和更改跟踪会话的属性

-   启用和禁用[跟踪提供程序](trace-provider.md)

-   刷新跟踪会话缓冲区

-   正在运行的 （实时） 跟踪会话的列表

-   列出了[注册的跟踪提供程序](registered-provider.md)

-   测量时间花在延缓过程调用 (Dpc) 和中断服务例程 (Isr)

Tracelog 生成包含提供程序跟踪会话期间生成的跟踪消息事件跟踪日志 (.etl) 文件。 消息存储在文件中的二进制格式。 若要以可读格式显示跟踪消息，请使用[TraceView](traceview.md)或[Tracefmt](tracefmt.md)。

Tracelog 内核模式和专用 （用户模式） 跟踪会话和特殊会话等控件[NT 内核记录器跟踪会话](nt-kernel-logger-trace-session.md)并[全局记录器跟踪会话](global-logger-trace-session.md)。

Tracelog 运行于 Windows 7 和更高版本的 Windows。

许多功能跟踪日志也会出现在[TraceView](traceview.md)，包含具有除了命令行界面的图形用户界面 Windows Driver Kit (WDK) 中的工具。

## <a name="span-idinthissectionspanin-this-section"></a><span id="in_this_section"></span>本部分中的内容

-   [**Tracelog 命令语法**](tracelog-command-syntax.md)
-   [Tracelog 显示](tracelog-displays.md)
-   [跟踪日志示例](tracelog-examples.md)
