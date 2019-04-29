---
title: 启动和退出 TraceView
description: 启动和退出 TraceView
ms.assetid: ebadf441-c28a-4d8e-ae83-444c8a68f62b
keywords:
- TraceView WDK 启动
- TraceView WDK，正在退出
- TraceView WDK，命令行接口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2c97ae0ddd275c3988108ab32d72be4cd2b64ec7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387908"
---
# <a name="starting-and-exiting-traceview"></a>启动和退出 TraceView


## <span id="ddk_starting_traceview_tools"></span><span id="DDK_STARTING_TRACEVIEW_TOOLS"></span>


本主题说明如何打开和关闭 TraceView 窗口。

### <a name="span-idstartingtraceviewspanspan-idstartingtraceviewspanstarting-traceview"></a><span id="starting_traceview"></span><span id="STARTING_TRACEVIEW"></span>起始 TraceView

若要启动 TraceView，在 Windows 资源管理器中，导航到\\工具\\跟踪\\i386 子目录的 WDK 和双击**TraceView.exe**图标。

或者，在命令提示符窗口中，导航到\\工具\\跟踪\\WDK 和类型的 i386 子目录**traceview**。

### <a name="span-idexitingtraceviewspanspan-idexitingtraceviewspanexiting-traceview"></a><span id="exiting_traceview"></span><span id="EXITING_TRACEVIEW"></span>退出 TraceView

若要在退出 TraceView，**文件**菜单上，单击**退出**，或单击 TraceView 窗口右上角的关闭按钮。

退出时 TraceView，它禁用跟踪提供程序中运行的跟踪会话，它启动，停止在 TraceView 窗口中，运行的所有跟踪会话，然后关闭。 此过程可能需要几秒钟即可完成，在此期间，Windows 可能会通知你 TraceView 未响应。 不强制 TraceView 准备就绪之前关闭。

退出 TraceView 不会停止跟踪会话通过其他方法，包括[TraceView 命令行界面](traceview-command-line-interface.md)。 这些会话将继续运行，直到你停止它们或关闭 Windows。

### <a name="span-idstartingthetraceviewcommandlineinterfacespanspan-idstartingthetraceviewcommandlineinterfacespanstarting-the-traceview-command-line-interface"></a><span id="starting_the_traceview_command_line_interface"></span><span id="STARTING_THE_TRACEVIEW_COMMAND_LINE_INTERFACE"></span>启动 TraceView 命令行接口

若要开始在命令行 TraceView，请打开命令提示符窗口，导航到\\工具\\跟踪\\i386 目录的 WDK，并键入 TraceView 命令，如**traceview /？**。 (如果键入**traceview**不带任何参数，TraceView 窗口随即打开。)

有关 TraceView 命令的信息，请参阅[TraceView 命令行界面](traceview-command-line-interface.md)。

 

 





