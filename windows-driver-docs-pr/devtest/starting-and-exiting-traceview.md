---
title: 启动和退出 TraceView
description: 启动和退出 TraceView
keywords:
- TraceView WDK，开始
- TraceView WDK，退出
- TraceView WDK，命令行界面
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a31431f6624dba04eaae9863c9530463a366d0df
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826641"
---
# <a name="starting-and-exiting-traceview"></a>启动和退出 TraceView


## <span id="ddk_starting_traceview_tools"></span><span id="DDK_STARTING_TRACEVIEW_TOOLS"></span>


本主题说明如何打开和关闭 "TraceView" 窗口。

### <a name="span-idstarting_traceviewspanspan-idstarting_traceviewspanstarting-traceview"></a><span id="starting_traceview"></span><span id="STARTING_TRACEVIEW"></span>启动 TraceView

若要启动 TraceView，请在 Windows 资源管理器中，导航到 \\ WDK 的工具 \\ 跟踪 \\ i386 子目录，然后双击 **TraceView.exe** 图标。

或者，在命令提示符窗口中，导航到 \\ WDK 的工具 \\ 跟踪 \\ i386 子目录，然后键入 **traceview**。

### <a name="span-idexiting_traceviewspanspan-idexiting_traceviewspanexiting-traceview"></a><span id="exiting_traceview"></span><span id="EXITING_TRACEVIEW"></span>正在退出 TraceView

若要退出 TraceView，请在 " **文件** " 菜单上，单击 " **退出**"，或单击 TraceView 窗口右上角的 "关闭" 按钮。

退出 TraceView 时，它将禁用正在启动的跟踪会话中运行的跟踪提供程序，停止正在 TraceView 窗口中运行的所有跟踪会话，然后关闭。 此过程可能需要几秒钟才能完成，在此过程中，Windows 可能会通知你 TraceView 未响应。 不要强制 TraceView 在准备就绪之前关闭。

退出 TraceView 不会停止由其他方法启动的跟踪会话，包括 [TraceView 命令行接口](traceview-command-line-interface.md)。 这些会话将继续运行，直到你停止它们或关闭 Windows。

### <a name="span-idstarting_the_traceview_command_line_interfacespanspan-idstarting_the_traceview_command_line_interfacespanstarting-the-traceview-command-line-interface"></a><span id="starting_the_traceview_command_line_interface"></span><span id="STARTING_THE_TRACEVIEW_COMMAND_LINE_INTERFACE"></span>启动 TraceView Command-Line 接口

若要在命令行中启动 TraceView，请打开命令提示符窗口，导航到 \\ WDK 的 tools \\ 跟踪 \\ i386 目录，然后键入 TraceView 命令，如 **TraceView/？**。  (如果键入 **traceview** 而不带参数，则 traceview 窗口打开。 ) 

有关 TraceView 命令的信息，请参阅 [TraceView Command-Line Interface](traceview-command-line-interface.md)。

 

 





