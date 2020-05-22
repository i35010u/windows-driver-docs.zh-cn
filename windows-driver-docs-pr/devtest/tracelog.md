---
title: Tracelog
description: Tracelog （Tracelog）是在命令提示符窗口中运行的事件跟踪控制器。 本部分介绍 Tracelog、说明其命令语法，并提供其使用情况的实际示例。
ms.assetid: aa3c144d-260b-44d2-b41c-d18be40ba541
keywords:
- Tracelog WDK
- 软件跟踪 WDK，Tracelog
- 跟踪 WDK，Tracelog
- 事件跟踪控制器 WDK Tracelog
- 跟踪会话管理 WDK Tracelog
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 72c16147dcc2390c6437060a92d692b91fec241f
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769565"
---
# <a name="tracelog"></a>Tracelog


Tracelog （Tracelog）是在命令提示符窗口中运行的事件跟踪控制器。 本部分介绍 Tracelog、说明其命令语法，并提供其使用情况的实际示例。

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
<td align="left"><p>安装 WDK、Visual Studio 和适用于桌面应用的 Windows SDK 时，将包含 Tracelog （Tracelog）。 有关下载套件的信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/download-the-wdk" data-raw-source="[Windows Hardware Downloads](https://docs.microsoft.com/windows-hardware/drivers/download-the-wdk)">Windows 硬件下载</a>。</p>
<p><strong>Windows 驱动程序工具包（WDK） 8</strong> （安装路径）</p>
<p>%WindowsSdkDir%\tools\x64\tracelog.exe</p>
<p>%WindowsSdkDir%\tools\x86\tracelog.exe</p>
<p><strong>Windows 驱动程序工具包（WDK） 8.1</strong> （安装路径）</p>
<p>%WindowsSdkDir%\bin\x64\tracelog.exe</p>
<p>%WindowsSdkDir%\bin\x86\tracelog.exe</p>
<div class="alert">
<strong>注意</strong>   Visual Studio 环境变量% WindowsSdkDir% 表示安装包的 Windows 工具包目录的路径，例如，C:\Program Files （x86） \Windows Kits\8.1。
</div>
</td>
</tr>
</tbody>
</table>

 

## <a name="span-idwhat_you_can_do_with_tracelogspanspan-idwhat_you_can_do_with_tracelogspanspan-idwhat_you_can_do_with_tracelogspanwhat-you-can-do-with-tracelog"></a><span id="What_you_can_do_with_Tracelog"></span><span id="what_you_can_do_with_tracelog"></span><span id="WHAT_YOU_CAN_DO_WITH_TRACELOG"></span>可以通过 Tracelog 执行的操作


可以在命令提示符窗口中使用 Tracelog 作为事件跟踪控制器。

**注意**   若要控制跟踪会话，您必须是计算机上 "Performance Log Users" 组或 "Administrators" 组的成员（以**管理员身份运行**）。

Tracelog 功能包括：

-   启动和停止[跟踪会话](trace-session.md)，包括专用跟踪会话、 [NT 内核记录器跟踪会话](nt-kernel-logger-trace-session.md)和[全局记录器跟踪会话](global-logger-trace-session.md)

-   配置和更改跟踪会话的属性

-   启用和禁用[跟踪提供程序](trace-provider.md)

-   刷新跟踪会话缓冲区

-   列出正在运行的（实时）跟踪会话

-   列出[注册的跟踪提供程序](registered-provider.md)

-   度量延迟的过程调用（Dpc）和中断服务例程（Isr）所用的时间

Tracelog 生成一个事件跟踪日志（.etl）文件，其中包含跟踪会话期间提供程序生成的跟踪消息。 消息以二进制格式存储在文件中。 若要以可读格式显示跟踪消息，请使用[TraceView](traceview.md)或[Tracefmt](tracefmt.md)。

Tracelog 控制内核模式和专用（用户模式）跟踪会话，以及特殊会话（如[NT 内核记录器跟踪会话](nt-kernel-logger-trace-session.md)和[全局记录器跟踪会话](global-logger-trace-session.md)）。

Tracelog 在 windows 7 和更高版本的 Windows 上运行。

[TraceView](traceview.md)中还提供了 Tracelog 的许多功能，包括在 Windows 驱动程序工具包（WDK）中的一种工具，该工具具有一个图形用户界面以及一个命令行界面。

## <a name="span-idin_this_sectionspanin-this-section"></a><span id="in_this_section"></span>本部分内容

-   [**Tracelog 命令语法**](tracelog-command-syntax.md)
-   [Tracelog 显示](tracelog-displays.md)
-   [Tracelog 示例](tracelog-examples.md)
