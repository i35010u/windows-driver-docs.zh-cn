---
title: Windows 调试工具中包含的工具
description: 适用于 Windows 的调试工具除了调试引擎和调试环境以外，还包括多个工具。 这些工具位于 Windows 调试工具的安装目录中。
ms.assetid: f5d761b9-866e-4948-978e-e95f8aed8b21
ms.date: 12/03/2019
ms.localizationpriority: medium
ms.openlocfilehash: 819c50b37d14a228af0d00da4678b05230fbabcb
ms.sourcegitcommit: b316c97bafade8b76d5d3c30d48496915709a9df
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "79242794"
---
# <a name="tools-included-in-debugging-tools-for-windows"></a>Windows 调试工具中包含的工具

适用于 Windows 的调试工具除了调试引擎和[调试环境](debuggers-in-the-debugging-tools-for-windows-package.md)以外，还包括多个工具。 这些工具位于 Windows 调试工具的[安装目录](#installation-directories)中。

## <span id="additional_tools_and_utilities"></span><span id="ADDITIONAL_TOOLS_AND_UTILITIES"></span>

<span id="DumpChk"></span><span id="dumpchk"></span><span id="DUMPCHK"></span>[DumpChk](dumpchk.md)  
验证内存转储文件。

<span id="GFlags"></span><span id="gflags"></span><span id="GFLAGS"></span>[GFlags](gflags.md)  
控制注册表项和其他设置。

<span id="Kill"></span><span id="kill"></span><span id="KILL"></span>[终止](kill-tool.md)  
终止进程。

<span id="Logger_and_LogViewer"></span><span id="logger_and_logviewer"></span><span id="LOGGER_AND_LOGVIEWER"></span>[记录器和 LogViewer](logger-and-logviewer.md)  
记录和显示程序的函数调用和其他操作。

<span id="PLMDebug"></span><span id="plmdebug"></span><span id="PLMDEBUG"></span>[PLMDebug](plmdebug.md)  
使用 Windows 调试器调试 Windows 应用程序，该应用程序在进程生命周期管理（PLM）下运行。 使用 PLMDebug，可以手动控制挂起、继续和终止 Windows 应用。

<span id="Remote_Tool"></span><span id="remote_tool"></span><span id="REMOTE_TOOL"></span>[远程工具](remote-tool.md)  
远程控制任何控制台程序，包括 KD、CDB 和 NTSD。 请参阅[通过远程调试](remote-debugging-through-remote-exe.md)的远程调试。

<span id="TList"></span><span id="tlist"></span><span id="TLIST"></span>[Tlist.exe](tlist.md)  
列出所有正在运行的进程。

<span id="UMDH"></span><span id="umdh"></span>[UMDH](umdh.md)  
分析堆分配。

<span id="USBView"></span><span id="usbview"></span><span id="USBVIEW"></span>[USBView](usbview.md)  
显示 USB 主机控制器和连接的设备。

<span id="dbgrpc___dbgrpc.exe_"></span><span id="DBGRPC___DBGRPC.EXE_"></span>DbgRpc （Dbgrpc）  
显示 Microsoft 远程过程调用（RPC）状态信息。 请参阅[RPC 调试](rpc-debugging.md)和[使用 DbgRpc 工具](using-the-dbgrpc-tool.md)。

<span id="kdbgctrl___kernel_debugging_control__kdbgctrl.exe_"></span><span id="KDBGCTRL___KERNEL_DEBUGGING_CONTROL__KDBGCTRL.EXE_"></span>KDbgCtrl （内核调试控件，Kdbgctrl）  
控制和配置内核调试连接。 请参阅[使用 KDbgCtrl](using-kdbgctrl.md)。

<span id="SrcSrv"></span><span id="srcsrv"></span><span id="SRCSRV"></span>[Srcsrv.ini](srcsrv.md)  
可用于在调试时传递源文件的源服务器。

<span id="SymSrv"></span><span id="symsrv"></span><span id="SYMSRV"></span>[SymSrv](symsrv.md)  
调试器可用于连接到符号存储区的符号服务器。

<span id="SymProxy"></span><span id="symproxy"></span><span id="SYMPROXY"></span>[SymProxy](symproxy.md)  
在网络上创建所有调试器都可以指向的单个 HTTP 符号服务器。 此方法的优点是指多个符号服务器（内部和外部）和单个符号路径，处理所有身份验证，并通过符号缓存提高性能。 Symproxy 位于[安装目录](#installation-directories)的 Symproxy 文件夹中。

<span id="SymChk"></span><span id="symchk"></span><span id="SYMCHK"></span>[SymChk](symchk.md)  
将可执行文件与符号文件进行比较，以验证正确的符号是否可用。

<span id="SymStore"></span><span id="symstore"></span><span id="SYMSTORE"></span>[SymStore](symstore.md)  
创建符号存储区。 请参阅[使用 SymStore](symstore.md)。

<span id="AgeStore"></span><span id="agestore"></span><span id="AGESTORE"></span>[AgeStore](agestore.md)  
删除符号服务器或源服务器的下游存储中的旧条目。

<span id="DBH"></span><span id="dbh"></span>[THIS->DBH](dbh.md)  
显示有关符号文件的内容的信息。

<span id="PDBCopy"></span><span id="pdbcopy"></span><span id="PDBCOPY"></span>[Pdbcopy.exe](pdbcopy.md)  
从符号文件中删除私有符号信息，并控制文件中包含的公共符号。

<span id="DbgSrv__"></span><span id="dbgsrv__"></span><span id="DBGSRV__"></span>DbgSrv   
用于远程调试的进程服务器。 请参阅[进程服务器（用户模式）](process-servers--user-mode-.md)。

<span id="KdSrv"></span><span id="kdsrv"></span><span id="KDSRV"></span>KdSrv  
用于远程调试的 KD 连接服务器。请参阅[KD 连接服务器（内核模式）](kd-connection-servers--kernel-mode-.md)。

<span id="DbEngPrx"></span><span id="dbengprx"></span><span id="DBENGPRX"></span>DbEngPrx  
用于远程调试的中继器（小型代理服务器）。 请参阅[中继器](repeaters.md)。

<span id="breakin___breakin.exe_"></span><span id="BREAKIN___BREAKIN.EXE_"></span>Breakin （Breakin）  
导致进程中发生用户模式中断。 若要获得帮助，请打开命令提示符窗口，导航到[安装目录](#installation-directories)，然后输入**breakin/？** 。

<span id="list___file_list_utility___list.exe_"></span><span id="LIST___FILE_LIST_UTILITY___LIST.EXE_"></span>列表（文件列表实用工具）（List .exe）  
若要获得帮助，请打开命令提示符窗口，导航到[安装目录](#installation-directories)，然后输入**list/？** 。

<span id="rtlist___remote_task_list_viewer___rtlist.exe_"></span><span id="RTLIST___REMOTE_TASK_LIST_VIEWER___RTLIST.EXE_"></span>RTList （远程任务列表查看器）（Rtlist）  
通过 DbgSrv 进程服务器列出正在运行的进程。 若要获得帮助，请打开命令提示符窗口，导航到[安装目录](#installation-directories)，然后输入**rtlist/？** 。

## <a name="span-idinstallation-directoriesspanspan-idinstallation-directoriesspaninstallation-directory"></a><span id="installation-directories"></span><span id="INSTALLATION-DIRECTORIES"></span>安装目录

对于调试工具，64位 OS 安装的默认安装目录为 C：\\Program Files （x86）\\Windows 工具包\\10\\调试器\\。 如果使用的是32位的操作系统，则可以在 "C：\\Program Files" 下找到 "Windows 工具包" 文件夹。 若要确定是否应使用32位或64位工具，请参阅[选择32位或64调试工具](choosing-a-32-bit-or-64-bit-debugger-package.md)。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题

[与 Windows 调试工具相关的工具](tools-related-to-debugging-tools-for-windows.md)
