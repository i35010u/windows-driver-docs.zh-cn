---
title: Tracelog
description: 'Tracelog ( # A0) 是在命令提示符窗口中运行的事件跟踪控制器。 本部分介绍 Tracelog、说明其命令语法，并提供其使用情况的实际示例。'
keywords:
- Tracelog WDK
- 软件跟踪 WDK，Tracelog
- 跟踪 WDK，Tracelog
- 事件跟踪控制器 WDK Tracelog
- 跟踪会话管理 WDK Tracelog
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a75ea0454067cca3d7ca5b11163cb4d827eeaef8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838123"
---
# <a name="tracelog"></a>Tracelog


Tracelog ( # A0) 是在命令提示符窗口中运行的事件跟踪控制器。 本部分介绍 Tracelog、说明其命令语法，并提供其使用情况的实际示例。

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">在哪里可以获得 Tracelog？</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>安装 WDK、Visual Studio 和桌面应用的 Windows SDK 时，将包含 Tracelog ( # A0) 。 有关下载工具包的信息，请参阅 <a href="/windows-hardware/drivers/download-the-wdk" data-raw-source="[Windows Hardware Downloads](../download-the-wdk.md)">Windows 硬件下载</a>。</p>
<p><strong>Windows 驱动程序工具包 (WDK) 8</strong> (安装路径) </p>
<p>% WindowsSdkDir% \tools\x64\tracelog.exe</p>
<p>% WindowsSdkDir% \tools\x86\tracelog.exe</p>
<p><strong>Windows 驱动程序工具包 (WDK) 8.1</strong> (安装路径) </p>
<p>% WindowsSdkDir% \bin\x64\tracelog.exe</p>
<p>% WindowsSdkDir% \bin\x86\tracelog.exe</p>
<div class="alert">
<strong>注意</strong>  Visual Studio 环境变量（%WindowsSdkDir%）表示安装了工具包的 Windows 工具包目录的路径，例如 C:\Program Files (x86)\Windows Kits\8.1。
</div>
</td>
</tr>
</tbody>
</table>

 

## <a name="span-idwhat_you_can_do_with_tracelogspanspan-idwhat_you_can_do_with_tracelogspanspan-idwhat_you_can_do_with_tracelogspanwhat-you-can-do-with-tracelog"></a><span id="What_you_can_do_with_Tracelog"></span><span id="what_you_can_do_with_tracelog"></span><span id="WHAT_YOU_CAN_DO_WITH_TRACELOG"></span>可以通过 Tracelog 执行的操作


可以在命令提示符窗口中使用 Tracelog 作为事件跟踪控制器。

**注意**  若要控制跟踪会话，你必须是性能日志用户组的成员，或者是计算机上的 "管理员" 组的成员 (" **以管理员身份运行** ") 。

Tracelog 功能包括：

-   启动和停止 [跟踪会话](trace-session.md)，包括专用跟踪会话、 [NT 内核记录器跟踪会话](nt-kernel-logger-trace-session.md)和 [全局记录器跟踪会话](global-logger-trace-session.md)

-   配置和更改跟踪会话的属性

-   启用和禁用 [跟踪提供程序](trace-provider.md)

-   刷新跟踪会话缓冲区

-    (实时) 跟踪会话运行的列表

-   列出 [注册的跟踪提供程序](registered-provider.md)

-   度量延迟过程调用所用的时间 (Dpc) 和中断服务例程 (Isr) 

Tracelog 生成一个事件跟踪日志 ( .etl) 文件，该文件包含在跟踪会话期间由提供程序生成的跟踪消息。 消息以二进制格式存储在文件中。 若要以可读格式显示跟踪消息，请使用 [TraceView](traceview.md) 或 [Tracefmt](tracefmt.md)。

Tracelog 控制内核模式和私有 (用户模式) 跟踪会话和特殊会话（如 [NT 内核记录器跟踪会话](nt-kernel-logger-trace-session.md) 和 [全局记录器跟踪会话](global-logger-trace-session.md)）。

Tracelog 在 windows 7 和更高版本的 Windows 上运行。

[TraceView](traceview.md)中还提供了 Tracelog 的许多功能，它是 Windows 驱动程序)  (工具包中包含的一种工具，该工具包含一个图形用户界面以及一个命令行界面。

## <a name="span-idin_this_sectionspanin-this-section"></a><span id="in_this_section"></span>本部分中的内容

-   [**Tracelog 命令语法**](tracelog-command-syntax.md)
-   [Tracelog 显示](tracelog-displays.md)
-   [Tracelog 示例](tracelog-examples.md)
