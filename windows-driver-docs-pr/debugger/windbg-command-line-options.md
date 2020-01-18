---
title: WinDbg 命令行选项
description: WinDbg 的首次用户应从使用 WinDbg 的调试开始。
ms.assetid: bd169c73-0a46-41b5-bd7b-71adf7747069
keywords:
- WinDbg 命令行选项 Windows 调试
ms.date: 08/10/2018
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
topic_type:
- apiref
api_name:
- WinDbg Command-Line Options
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 304e083f7220234ea55f997527fa5ad3a25f9be2
ms.sourcegitcommit: 6d930ed810124ade8e29a617c7abcd399113696f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/17/2020
ms.locfileid: "76256749"
---
# <a name="windbg-command-line-options"></a>WinDbg 命令行选项

WinDbg 的首次用户应从[使用 WinDbg 的调试](debugging-using-windbg.md)开始。

WinDbg 命令行使用以下语法：

```dbgsyntax
windbg [ -server ServerTransport | -remote ClientTransport ] [-lsrcpath ]
   [ -premote SmartClientTransport ] [-?] [-ee {masm|c++}] 
   [-clines lines] [-b] [-d] [-aExtension]  
   [-failinc] [-g] [-G] [-hd] [-j] [-n] [-noshell] [-o] [-openPrivateDumpByHandle Handle]
   [-Q | -QY] [-QS | -QSY] [-robp] [-secure] [-ses] [-sdce] 
   [-sicv] [-sins] [-snc] [-snul] [-sup] [-sflags 0xNumber] 
   [-T Title] [-v] [-log{o|a} LogFile] [-noinh] 
   [-i ImagePath] [-y SymbolPath] [-srcpath SourcePath] 
   [-k [ConnectType] | -kl | -kx ExdiOptions] [-c "command"] 
   [-pb] [-pd] [-pe] [-pr] [-pt Seconds] [-pv]
   [-W Workspace] [-WF Filename] [-WX] [-zp PageFile] 
   [ -p PID | -pn Name | -psn ServiceName | -z DumpFile | executable ] 

windbg -I[S] 

windbg -IU KeyString

windbg -IA[S] 
```

有关 WinDbg 命令行选项的说明，请参阅。 所有命令行选项都区分大小写，但**j**除外。 可以使用正斜杠（/）替换初始连字符。

如果使用了 **-remote**或 **-server**选项，则它必须出现在命令行上的任何其他选项之前。 如果指定了*可执行文件*，则它必须出现在命令行的最后;*可执行文件*名称后的任何文本都作为其自身的命令行参数传递给可执行程序。

## <a name="span-idddk_windbg_command_line_options_dbgspanspan-idddk_windbg_command_line_options_dbgspanparameters"></a><span id="ddk_windbg_command_line_options_dbg"></span><span id="DDK_WINDBG_COMMAND_LINE_OPTIONS_DBG"></span>Parameters


<span id="_______-server_______ServerTransport______"></span><span id="_______-server_______servertransport______"></span><span id="_______-SERVER_______SERVERTRANSPORT______"></span> **-server** *ServerTransport*   
创建可由其他调试器访问的调试服务器。 有关可能的*ServerTransport*值的说明，请参阅[**激活调试服务器**](activating-a-debugging-server.md)。 使用此参数时，该参数必须是命令行中的第一个参数。

<span id="_______-remote_______ClientTransport______"></span><span id="_______-remote_______clienttransport______"></span><span id="_______-REMOTE_______CLIENTTRANSPORT______"></span> **-remote** *ClientTransport*   
创建调试客户端，并连接到已在运行的调试服务器。 有关可能的*ClientTransport*值的说明，请参阅[**激活调试客户端**](activating-a-debugging-client.md)。 使用此参数时，该参数必须是命令行中的第一个参数。

<span id="_______-premote_______SmartClientTransport______"></span><span id="_______-premote_______smartclienttransport______"></span><span id="_______-PREMOTE_______SMARTCLIENTTRANSPORT______"></span> **-premote** *SmartClientTransport*   
创建智能客户端，并连接到已在运行的进程服务器。 有关可能的*SmartClientTransport*值的说明，请参阅[**激活智能客户端**](activating-a-smart-client.md)。

<span id="_______-a________Extension______"></span><span id="_______-a________extension______"></span><span id="_______-A________EXTENSION______"></span> **-** *扩展*   
设置默认扩展 DLL。 默认值为 kdextx86 或 kdexts。 "A" 后面一定不能有空格，并且不得包含 .dll 文件扩展名。 有关详细信息和设置此默认设置的其他方法，请参阅[加载调试器扩展 dll](loading-debugger-extension-dlls.md)。

<span id="_______-b______"></span><span id="_______-B______"></span> **-b**   
不再支持此选项。

<span id="_______-c_________command______________"></span><span id="_______-C_________COMMAND______________"></span> **-c "** *command* **"**    
指定要在启动时运行的初始调试器命令。 此命令必须用引号引起来。 可以用分号分隔多个命令。 （如果您有一个长命令列表，则可以更容易地将其放入脚本，然后将 **-c**选项与[ **$&lt;，$&gt;&lt;，$&gt;&lt;，$ $&gt;&lt; （运行脚本文件）** ](-----------------------a---run-script-file-.md)命令一起使用。）

如果要启动调试客户端，则必须将此命令用于调试服务器。 不允许使用客户端特定的命令（如**lsrcpath**）。

<span id="_______-clines________lines______"></span><span id="_______-CLINES________LINES______"></span> **-clines** *行*   
设置在远程调试过程中可以访问的命令历史记录中的大概命令数。 有关详细信息以及其他更改此数字的方法，请参阅[使用调试器命令](using-debugger-commands.md)。

<span id="_______-d______"></span><span id="_______-D______"></span> **-d**   
（仅限内核模式）重新启动后，只要加载内核模块，调试器就会进入目标计算机。 （此中断早于 **-b**选项的 break。）有关详细信息和其他更改此状态的方法，请参阅[崩溃并重新启动目标计算机](crashing-and-rebooting-the-target-computer.md)。

<span id="_______-ee__masm_c___"></span><span id="_______-EE__MASM_C___"></span> **-ee** {**masm**|**c + +** }  
设置默认表达式计算器。 如果指定了**masm** ，将使用 masm 表达式语法。 如果指定**c + +** ， C++则使用 expression 语法。 如果省略 **-ee**选项，则将使用 MASM 表达式语法作为默认值。 有关详细信息，请参阅[计算表达式](evaluating-expressions.md)。

<span id="_______-failinc______"></span><span id="_______-FAILINC______"></span> **-failinc**   
导致调试器忽略任何有问题的符号。 调试用户模式或内核模式小型转储文件时，此选项还会阻止调试器加载其图像无法映射的任何模块。 有关详细信息和控制此方法的其他方法，请参阅[SYMOPT\_精确\_符号](symbol-options.md#symopt-exact-symbols)。

<span id="_______-g______"></span><span id="_______-G______"></span> **-g**   
（仅用户模式）忽略目标应用程序中的初始断点。 如果已设置了另一个断点，则此选项将导致目标应用程序在启动后继续运行或将 WinDbg 附加到该应用程序。 有关详细信息，请参阅[初始断点](initial-breakpoint.md)。

<span id="_______-G______"></span><span id="_______-g______"></span> **-G**   
（仅用户模式）在进程终止时忽略最终断点。 通常，调试会话在映像运行过程中结束。 此选项将导致调试会话在子项终止时立即结束。 这与输入命令**sxd epr**相同。 有关详细信息，请参阅[控制异常和事件](controlling-exceptions-and-events.md)。

<span id="_______-hd______"></span><span id="_______-HD______"></span> **-hd**   
（仅用户模式）指定不应使用调试堆。

<span id="_______-I_S_"></span><span id="_______-i_s_"></span> **-I**\[**S**\]  
将 WinDbg 安装为事后调试器。 有关详细信息，请参阅[启用事后调试](enabling-postmortem-debugging.md)。

尝试执行此操作后，会显示成功或失败消息。 如果包含，则此过程将以无提示方式完成 **，如果成功**，则为;仅显示失败消息。

**-I**参数不得与任何其他参数一起使用。 此命令实际上不会启动 WinDbg，但此时可能会出现一个 WinDbg 窗口。

<span id="_______-IA_S_"></span><span id="_______-ia_s_"></span> **-IA**\[**S**\]  
将 WinDbg 与注册表中的文件扩展名 dmp、.mdmp 和 wew 相关联。 尝试执行此操作后，会显示成功或失败消息。 如果包含，则此过程将以无提示方式完成 **，如果成功**，则为;仅显示失败消息。 建立此关联后，双击具有其中一个扩展的文件将启动 WinDbg。

**-IA**参数不得与任何其他参数一起使用。 此命令实际上不会启动 WinDbg，但此时可能会出现一个 WinDbg 窗口。

<span id="_______-IU________KeyString______"></span><span id="_______-iu________keystring______"></span><span id="_______-IU________KEYSTRING______"></span> **-IU** *KeyString*   
将调试器远程处理注册为 URL 类型，以便用户可以使用 URL 自动启动调试器远程客户端。 *KeyString*的格式 `remdbgeng://RemotingOption`。 *RemotingOption*是一个字符串，它定义在[**激活调试客户端**](activating-a-debugging-client.md)主题中定义的传输协议。 如果此操作成功，则不会显示任何消息;如果失败，将显示一条错误消息。

**-IU**参数不得与任何其他参数一起使用。 尽管某个 WinDbg 窗口可能会显示一段时间，但此命令实际上不会启动 WinDbg。

<span id="_______-i_______ImagePath______"></span><span id="_______-i_______imagepath______"></span><span id="_______-I_______IMAGEPATH______"></span> **-i** *ImagePath*   
指定生成错误的可执行文件的位置。 如果路径包含空格，则应该用引号将其引起来。

<span id="_______-j______"></span><span id="_______-J______"></span> **-j**   
允许日志记录。

<span id="_______-k__ConnectType_"></span><span id="_______-k__connecttype_"></span><span id="_______-K__CONNECTTYPE_"></span> **-k** \[*ConnectType*\]  
（仅限内核模式）启动内核调试会话。 有关详细信息，请参阅[使用 WinDbg 进行实时内核模式调试](performing-kernel-mode-debugging-using-windbg.md)。 如果使用 **-k**而没有任何*ConnectType*选项，则它必须是命令行中的最后一个条目。

<span id="_______-kl______"></span><span id="_______-KL______"></span> **-kl**   
（仅限内核模式）在调试器所在的同一台计算机上启动内核调试会话。

<span id="_______-kx_______ExdiOptions______"></span><span id="_______-kx_______exdioptions______"></span><span id="_______-KX_______EXDIOPTIONS______"></span> **-kx** *ExdiOptions*   
（仅限内核模式）使用 EXDI 驱动程序启动内核调试会话。 本文档未介绍 EXDI 驱动程序。 如果你的硬件探测或硬件模拟器具有 EXDI 接口，请联系 Microsoft 以获取调试信息。

<span id="_______-log_o_a__LogFile"></span><span id="_______-log_o_a__logfile"></span><span id="_______-LOG_O_A__LOGFILE"></span> **-log**{**o**| **}** 日志*文件*  
开始将信息记录到日志文件。 如果指定的日志文件已存在，则在使用**徽标**时将覆盖它。 如果使用了**loga** ，则输出将追加到该文件。 有关更多详细信息，请参阅[在 WinDbg 中保留日志文件](keeping-a-log-file-in-windbg.md)。

<span id="_______-lsrcpath______"></span><span id="_______-LSRCPATH______"></span> **-lsrcpath**   
设置远程客户端的本地源路径。 此选项必须在命令行的后面跟**远程**。

<span id="_______-n______"></span><span id="_______-N______"></span> **-n**   
*干扰符号加载*：从符号处理程序启用详细输出。 有关详细信息和控制此方法的其他方法，请参阅[SYMOPT\_调试](symbol-options.md#symopt-debug)。

<span id="_______-noinh______"></span><span id="_______-NOINH______"></span> **-noinh**   
（仅用户模式）阻止调试器创建的进程从调试器继承句柄。 有关控制此操作的其他方法，请参阅[使用 WinDbg 调试用户模式进程](debugging-a-user-mode-process-using-windbg.md)。

<span id="_______-noprio______"></span><span id="_______-NOPRIO______"></span> **-noprio**   
禁止任何优先级更改。 此参数将阻止 WinDbg 在活动期间为 CPU 时间取优先级。

<span id="_______-noshell______"></span><span id="_______-NOSHELL______"></span> **-noshell**   
禁止全部**shell**命令。 即使启动了新的调试会话，此禁止仍将在调试器运行的时间结束。 有关详细信息，以及其他禁用 shell 命令的方法，请参阅[使用 Shell 命令](using-shell-commands.md)。

<span id="_______-o______"></span><span id="_______-O______"></span> **-o**   
（仅用户模式）调试由目标应用程序启动的所有进程（子进程）。 默认情况下，由正在调试的进程创建的进程将按正常运行的方式运行。

<span id="_______-openPrivateDumpByHandle______"></span><span id="_______-OPENPRIVATEDUMPBYHANDLE______"></span> **-openPrivateDumpByHandle** *句柄*   
指定要调试的故障转储文件的句柄。

<span id="_______-p_______PID______"></span><span id="_______-p_______pid______"></span><span id="_______-P_______PID______"></span> **-p** *PID*   
指定要调试的十进制进程 ID。 这用于调试已经在运行的进程。

<span id="_______-pb______"></span><span id="_______-PB______"></span> **-pb**   
（仅用户模式）阻止调试器在附加到目标进程时请求初始中断。 如果应用程序已挂起，或者您想要避免在目标中创建一个中断线程，这会很有用。

<span id="_______-pd______"></span><span id="_______-PD______"></span> **-pd**   
（仅用户模式）使目标应用程序不会在调试会话结束时终止。 有关详细信息，请参阅[在 WinDbg 结束调试会话](ending-a-debugging-session-in-windbg.md)。

<span id="_______-pe______"></span><span id="_______-PE______"></span> **-pe**   
（仅用户模式）指示目标应用程序已在进行调试。 有关详细信息，请参阅[重新附加到目标应用程序](reattaching-to-the-target-application.md)。

<span id="_______-pn_______Name______"></span><span id="_______-pn_______name______"></span><span id="_______-PN_______NAME______"></span> **-pn** *Name*   
指定要调试的进程的名称。 （此名称必须是唯一的。）这用于调试已经在运行的进程。

<span id="_______-pr______"></span><span id="_______-PR______"></span> **-pr**   
（仅用户模式）导致调试器在附加到目标进程时启动该进程。 这在应用程序已挂起且你希望它恢复执行时非常有用。

<span id="_______-psn_______ServiceName______"></span><span id="_______-psn_______servicename______"></span><span id="_______-PSN_______SERVICENAME______"></span> **-psn** *ServiceName*   
指定要调试的进程中包含的服务的名称。 这用于调试已经在运行的进程。

<span id="_______-pt_______Seconds______"></span><span id="_______-pt_______seconds______"></span><span id="_______-PT_______SECONDS______"></span> **-pt** *秒*   
指定中断超时（以秒为单位）。 默认值为 30。 有关详细信息，请参阅[控制目标](controlling-the-target.md)。

<span id="_______-pv______"></span><span id="_______-PV______"></span> **-pv**   
（仅用户模式）指定调试器应附加到目标进程 noninvasively。 有关详细信息，请参阅[Noninvasive 调试（用户模式）](noninvasive-debugging--user-mode-.md)。

<span id="_______-Q______"></span><span id="_______-q______"></span> **-Q**   
禁止显示 "保存工作区？" 对话框中指定选项。 不会自动保存工作区。 有关详细信息，请参阅[使用工作区](using-workspaces.md)。

<span id="_______-QS______"></span><span id="_______-qs______"></span> **-QS**   
禁止显示 "重载源？" 对话框中指定选项。 不会自动重新加载源文件。

<span id="_______-QSY______"></span><span id="_______-qsy______"></span> **-QSY**   
禁止显示 "重载源？" 对话框并自动重新加载源文件。

<span id="_______-QY______"></span><span id="_______-qy______"></span> **-QY**   
禁止显示 "保存工作区？" 对话框并自动保存工作区。 有关详细信息，请参阅[使用工作区](using-workspaces.md)。

<span id="_______-robp______"></span><span id="_______-ROBP______"></span> **-robp**   
这允许 CDB 在只读内存页面上设置断点。 （此类操作的默认值为失败。）

<span id="_______-sdce______"></span><span id="_______-SDCE______"></span> **-sdce**   
使调试器在符号加载过程中显示**文件访问错误**消息。 有关详细信息，请参阅[SYMOPT\_失败\_严重\_错误](symbol-options.md#symopt-fail-critical-errors)。

<span id="_______-secure______"></span><span id="_______-SECURE______"></span> **-secure**   
激活[安全模式](secure-mode.md)。

<span id="_______-ses______"></span><span id="_______-SES______"></span> **-ses**   
使调试器对所有符号文件执行严格的评估，并忽略任何有问题的符号。 有关详细信息和控制此方法的其他方法，请参阅[SYMOPT\_精确\_符号](symbol-options.md#symopt-exact-symbols)。

<span id="_______-sflags_0x________Number______"></span><span id="_______-sflags_0x________number______"></span><span id="_______-SFLAGS_0X________NUMBER______"></span> **-sflags 0x** *Number*   
同时设置所有符号处理程序选项。 *Number*应为以**0x**开头的十六进制数字，不允许使用**0x** ，但符号选项是二进制标志，因此建议使用十六进制。 应谨慎使用此选项，因为它将覆盖所有符号处理程序默认值。 有关详细信息，请参阅[设置符号选项](symbol-options.md)。

<span id="_______-sicv______"></span><span id="_______-SICV______"></span> **-sicv**   
导致符号处理程序忽略 CV 记录。 有关详细信息和控制此方法的其他方法，请参阅[SYMOPT\_IGNORE\_CVREC](symbol-options.md#symopt-ignore-cvrec)。

<span id="_______-sins______"></span><span id="_______-SINS______"></span> **-问题**   
导致调试器忽略符号路径和可执行图像路径环境变量。 有关详细信息，请参阅[SYMOPT\_IGNORE\_NT\_SYMPATH](symbol-options.md#symopt-ignore-nt-sympath)。

<span id="_______-snc______"></span><span id="_______-SNC______"></span> **-snc**   
使调试器关闭C++转换。 有关详细信息和控制此方法的其他方法，请参阅[SYMOPT\_no\_CPP](symbol-options.md#symopt-no-cpp)。

<span id="_______-snul______"></span><span id="_______-SNUL______"></span> **-snul**   
为非限定名称禁用自动符号加载。 有关详细信息和控制此方法的其他方法，请参阅[SYMOPT\_未\_未限定的\_负载](symbol-options.md#symopt-no-unqualified-loads)。

<span id="_______-srcpath_______SourcePath______"></span><span id="_______-srcpath_______sourcepath______"></span><span id="_______-SRCPATH_______SOURCEPATH______"></span> **-srcpath** *SourcePath*   
指定源文件搜索路径。 使用分号（ **;** ）分隔多个路径。 如果路径包含空格，则应该用引号将其引起来。 有关详细信息，请参阅[源路径](source-path.md)。

<span id="_______-sup______"></span><span id="_______-SUP______"></span> **-sup**   
使符号处理程序在每个符号搜索过程中搜索公共符号表。 有关详细信息和控制此方法的其他方法，请参阅[SYMOPT\_AUTO\_PUBLICS](symbol-options.md#symopt-auto-publics)。

<span id="_______-T_______Title______"></span><span id="_______-t_______title______"></span><span id="_______-T_______TITLE______"></span> **-T** *标题*   
设置 WinDbg 窗口标题。

<span id="_______-v______"></span><span id="_______-V______"></span> **-v**   
从调试器启用详细输出。

<span id="_______-W_______Workspace______"></span><span id="_______-w_______workspace______"></span><span id="_______-W_______WORKSPACE______"></span> **-W** *工作区*   
加载给定的命名工作区。 如果工作区名称包含空格，则用引号将其引起来。 如果此名称的工作区不存在，则会向你提供使用此名称创建新工作区或放弃加载尝试的选项。 有关详细信息，请参阅[使用工作区](using-workspaces.md)。

<span id="_______-WF_______Filename______"></span><span id="_______-wf_______filename______"></span><span id="_______-WF_______FILENAME______"></span> **-WF** *文件名*   
从给定文件加载工作区。 *Filename*应包括文件和扩展名（通常为 wew）。 如果工作区名称包含空格，则用引号将其引起来。 如果不存在具有此名称的工作区文件，则将向你提供使用此名称创建新的工作区文件或放弃加载尝试的选项。 有关详细信息，请参阅[使用工作区](using-workspaces.md)。

<span id="_______-WX______"></span><span id="_______-wx______"></span> **-WX**   
禁用自动工作区加载。 有关详细信息，请参阅[使用工作区](using-workspaces.md)。

<span id="_______-y_______SymbolPath______"></span><span id="_______-y_______symbolpath______"></span><span id="_______-Y_______SYMBOLPATH______"></span> **-y** *SymbolPath*   
指定符号搜索路径。 使用分号（ **;** ）分隔多个路径。 如果路径包含空格，则应该用引号将其引起来。 有关详细信息和更改此路径的其他方式，请参阅[符号路径](symbol-path.md)。

<span id="_______-z_______DumpFile______"></span><span id="_______-z_______dumpfile______"></span><span id="_______-Z_______DUMPFILE______"></span> **-z** *DumpFile*   
指定要调试的故障转储文件的名称。 如果路径和文件名包含空格，则必须用引号将其引起来。 可以通过包含多个**z**选项来一次打开多个转储文件，每个转储文件后跟不同的*DumpFile*值。 有关详细信息，请参阅[分析用户模式转储文件](analyzing-a-user-mode-dump-file.md)或[使用 WinDbg 分析内核模式转储文件](analyzing-a-kernel-mode-dump-file-with-windbg.md)。

<span id="_______-zp_______PageFile______"></span><span id="_______-zp_______pagefile______"></span><span id="_______-ZP_______PAGEFILE______"></span> **-zp** *页面文件*   
指定已修改的页面文件的名称。 如果正在调试转储文件，并且想要使用[**pagein （内存中的页）** ](-pagein--page-in-memory-.md)命令，此方法非常有用。 不能将 **-zp**与标准 Windows 页面文件一起使用，只能使用经过特别修改的页面文件。

<span id="_______executable______"></span><span id="_______EXECUTABLE______"></span>*可执行*   
指定可执行进程的命令行。 此操作用于启动新进程并对其进行调试。 这必须是命令行上的最后一项。 可执行文件名称后的所有文本都作为其参数字符串传递到可执行文件。 有关详细信息，请参阅[使用 WinDbg 调试用户模式进程](debugging-a-user-mode-process-using-windbg.md)。

<span id="_______-_______"></span> **-?**    
弹出此 HTML 帮助窗口。

在从命令行运行调试器时，请在应用程序的文件名后指定目标应用程序的参数。 例如：

```dbgcmd
windbg myexe arg1 arg2
```

 

 





