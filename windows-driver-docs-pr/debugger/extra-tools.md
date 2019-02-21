---
title: Windows 调试工具中包含的工具
description: 调试工具的 Windows 包括除了调试引擎和调试环境的多个工具。 这些工具包括有关 Windows 调试工具的安装目录中。
ms.assetid: f5d761b9-866e-4948-978e-e95f8aed8b21
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4ac79b379f2c1ea9221070f250af9a1b8d44cd84
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521570"
---
# <a name="tools-included-in-debugging-tools-for-windows"></a>Windows 调试工具中包含的工具


调试工具的 Windows 包含除了调试引擎的多种工具和[调试环境](debuggers-in-the-debugging-tools-for-windows-package.md)。 这些工具位于[安装目录](#installation-directories)的有关 Windows 调试工具。

## <span id="additional_tools_and_utilities"></span><span id="ADDITIONAL_TOOLS_AND_UTILITIES"></span>


<span id="ADPlus"></span><span id="adplus"></span><span id="ADPLUS"></span>[ADPlus](adplus.md)  
自动创建内存转储文件，并使用从一个或多个进程的调试输出日志文件。

<span id="DumpChk"></span><span id="dumpchk"></span><span id="DUMPCHK"></span>[DumpChk](dumpchk.md)  
验证内存转储文件。

<span id="GFlags"></span><span id="gflags"></span><span id="GFLAGS"></span>[GFlags](gflags.md)  
控制注册表项和其他设置。

<span id="Kill"></span><span id="kill"></span><span id="KILL"></span>[Kill](kill-tool.md)  
终止进程。

<span id="Logger_and_LogViewer"></span><span id="logger_and_logviewer"></span><span id="LOGGER_AND_LOGVIEWER"></span>[记录器和日志查看器](logger-and-logviewer.md)  
记录并显示函数调用和程序的其他操作。

<span id="PLMDebug"></span><span id="plmdebug"></span><span id="PLMDEBUG"></span>[PLMDebug](plmdebug.md)  
使用 Windows 调试器调试 Windows 应用，它运行在进程生命周期管理 (PLM)。 PLMDebug，与可能需要手动控制的挂起、 恢复和终止一个 Windows 应用程序。

<span id="Remote_Tool"></span><span id="remote_tool"></span><span id="REMOTE_TOOL"></span>[远程工具](remote-tool.md)  
远程控制任何控制台程序，包括 KD、 CDB 和 NTSD。 请参阅[Remote.exe 通过远程调试](remote-debugging-through-remote-exe.md)。

<span id="TList"></span><span id="tlist"></span><span id="TLIST"></span>[TList](tlist.md)  
列出所有正在运行的进程。

<span id="UMDH"></span><span id="umdh"></span>[UMDH](umdh.md)  
分析堆分配。

<span id="USBView"></span><span id="usbview"></span><span id="USBVIEW"></span>[USBView](usbview.md)  
显示 USB 主控制器和连接的设备。

<span id="dbgrpc___dbgrpc.exe_"></span><span id="DBGRPC___DBGRPC.EXE_"></span>DbgRpc (Dbgrpc.exe)  
显示 Microsoft 远程过程调用 (RPC) 的状态信息。 请参阅[RPC 调试](rpc-debugging.md)并[使用 DbgRpc 工具](using-the-dbgrpc-tool.md)。

<span id="kdbgctrl___kernel_debugging_control__kdbgctrl.exe_"></span><span id="KDBGCTRL___KERNEL_DEBUGGING_CONTROL__KDBGCTRL.EXE_"></span>KDbgCtrl （内核调试控件，Kdbgctrl.exe）  
控制和配置内核调试连接。 请参阅[使用 KDbgCtrl](using-kdbgctrl.md)。

<span id="SrcSrv"></span><span id="srcsrv"></span><span id="SRCSRV"></span>[SrcSrv](srcsrv.md)  
可用于在调试时传送源文件源服务器。

<span id="SymSrv"></span><span id="symsrv"></span><span id="SYMSRV"></span>[SymSrv](symsrv.md)  
符号服务器，调试器可以用来连接到符号存储区。

<span id="SymProxy"></span><span id="symproxy"></span><span id="SYMPROXY"></span>[SymProxy](symproxy.md)  
所有调试器可以都指向在网络上创建单个 HTTP 符号服务器。 这样做的好处的指向单个符号路径的多个符号服务器 （内部和外部），处理所有身份验证，提高通过符号缓存的性能。 位于 SymProxy 文件夹中 Symproxy.dll[安装目录](#installation-directories)。

<span id="SymChk"></span><span id="symchk"></span><span id="SYMCHK"></span>[SymChk](symchk.md)  
要验证提供了正确的符号的符号文件的可执行文件进行比较。

<span id="SymStore"></span><span id="symstore"></span><span id="SYMSTORE"></span>[SymStore](symstore.md)  
创建符号存储区。 请参阅[使用 SymStore](symstore.md)。

<span id="AgeStore"></span><span id="agestore"></span><span id="AGESTORE"></span>[AgeStore](agestore.md)  
符号服务器或源服务器的下游存储区中删除旧的条目。

<span id="DBH"></span><span id="dbh"></span>[DBH](dbh.md)  
显示符号文件的内容的信息。

<span id="PDBCopy"></span><span id="pdbcopy"></span><span id="PDBCOPY"></span>[PDBCopy](pdbcopy.md)  
删除私有符号信息符号文件，并控制文件中包含的公共符号。

<span id="DbgSrv__"></span><span id="dbgsrv__"></span><span id="DBGSRV__"></span>DbgSrv   
使用进行远程调试的进程服务器。 请参阅[进程服务器 （用户模式）](process-servers--user-mode-.md)。

<span id="KdSrv"></span><span id="kdsrv"></span><span id="KDSRV"></span>KdSrv  
使用进行远程调试的 KD 连接服务器。请参阅[KD 连接服务器 （内核模式）](kd-connection-servers--kernel-mode-.md)。

<span id="DbEngPrx"></span><span id="dbengprx"></span><span id="DBENGPRX"></span>DbEngPrx  
用于远程调试 repeater （较小的代理服务器）。 请参阅[重复字符](repeaters.md)。

<span id="breakin___breakin.exe_"></span><span id="BREAKIN___BREAKIN.EXE_"></span>Breakin (Breakin.exe)  
会导致用户模式下中断发生在进程中。 有关帮助，请打开命令提示符窗口，导航到[安装目录](#installation-directories)，并输入**breakin /？**。

<span id="list___file_list_utility___list.exe_"></span><span id="LIST___FILE_LIST_UTILITY___LIST.EXE_"></span>列表 （文件列表实用程序） (List.exe)  
有关帮助，请打开命令提示符窗口，导航到[安装目录](#installation-directories)，并输入**列表 /？**。

<span id="rtlist___remote_task_list_viewer___rtlist.exe_"></span><span id="RTLIST___REMOTE_TASK_LIST_VIEWER___RTLIST.EXE_"></span>RTList （远程任务列表查看器） (Rtlist.exe)  
通过 DbgSrv 进程服务器正在运行的进程的列表。 有关帮助，请打开命令提示符窗口，导航到[安装目录](#installation-directories)，并输入**rtlist /？**。

## <a name="span-idinstallation-directoriesspanspan-idinstallation-directoriesspaninstallation-directory"></a><span id="installation-directories"></span><span id="INSTALLATION-DIRECTORIES"></span>安装目录


调试工具的 64 位操作系统安装的默认安装目录为 c:\\Program Files (x86)\\Windows 工具包\\10\\调试器\\。 如果有 32 位操作系统，可以找到在 c: Windows Kits 文件夹\\程序文件。 若要确定是否应使用 32 位或 64 位工具，请参阅[选择 32 位或 64 位调试工具](choosing-a-32-bit-or-64-bit-debugger-package.md)。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


[对于 Windows 调试工具与相关的工具](tools-related-to-debugging-tools-for-windows.md)

 

 






