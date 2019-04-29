---
title: WinDbg 命令行选项
description: 第一次的 WinDbg 的用户应开始学习调试使用 WinDbg 部分。
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
ms.openlocfilehash: 19eed1e5fb64ace386790a202ac1542bb231750d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325838"
---
# <a name="windbg-command-line-options"></a>WinDbg 命令行选项


WinDbg 的第一次用户应开头[调试使用 WinDbg](debugging-using-windbg.md)部分。

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

按照 WinDbg 命令行选项的说明。 所有命令行选项都区分大小写除外 **-j**。 可以使用正斜杠 （/） 替换初始的连字符。

如果**的远程**或 **-server**选项，则它必须出现在之前在命令行上的任何其他选项。 如果*可执行文件*指定，则它必须显示命令行中的最后一个之后的任何文本*可执行文件*名称作为其自己的命令行参数传递给可执行程序。

## <a name="span-idddkwindbgcommandlineoptionsdbgspanspan-idddkwindbgcommandlineoptionsdbgspanparameters"></a><span id="ddk_windbg_command_line_options_dbg"></span><span id="DDK_WINDBG_COMMAND_LINE_OPTIONS_DBG"></span>参数


<span id="_______-server_______ServerTransport______"></span><span id="_______-server_______servertransport______"></span><span id="_______-SERVER_______SERVERTRANSPORT______"></span> **-server** *ServerTransport*   
创建可由其他调试器的调试服务器。 有关可能的说明*服务器传送*值，请参阅[**激活调试服务器**](activating-a-debugging-server.md)。 如果使用此参数，它必须是命令行中的第一个参数。

<span id="_______-remote_______ClientTransport______"></span><span id="_______-remote_______clienttransport______"></span><span id="_______-REMOTE_______CLIENTTRANSPORT______"></span> **-remote** *ClientTransport*   
创建调试客户端，并连接到已在运行的调试服务器。 有关可能的说明*ClientTransport*值，请参阅[**激活调试客户端**](activating-a-debugging-client.md)。 如果使用此参数，它必须是命令行中的第一个参数。

<span id="_______-premote_______SmartClientTransport______"></span><span id="_______-premote_______smartclienttransport______"></span><span id="_______-PREMOTE_______SMARTCLIENTTRANSPORT______"></span> **-premote** *SmartClientTransport*   
创建智能客户端，并连接到已在运行的进程服务器。 有关可能的说明*SmartClientTransport*值，请参阅[**激活智能客户端**](activating-a-smart-client.md)。

<span id="_______-a________Extension______"></span><span id="_______-a________extension______"></span><span id="_______-A________EXTENSION______"></span> **-a** *扩展*   
设置默认扩展插件 DLL。 默认值为 kdextx86.dll 或 kdexts.dll。 必须有后的没有空格不能包含"a"、 和.dll 文件扩展名。 有关详细信息，并设置此默认设置的其他方法，请参阅[加载的调试器扩展 Dll](loading-debugger-extension-dlls.md)。

<span id="_______-b______"></span><span id="_______-B______"></span> **-b**   
不再支持此选项。

<span id="_______-c_________command______________"></span><span id="_______-C_________COMMAND______________"></span> **-c "** *command* **"**   
指定要在启动时运行的初始调试器命令。 此命令必须括在引号中。 可以用分号分隔多个命令。 (如果有很长的命令列表，可能会更容易将其放在一个脚本，然后使用 **-c**选项与[  **$ &lt;，$&gt;&lt;，$&gt; &lt;，$$&gt; &lt; （运行脚本文件）** ](-----------------------a---run-script-file-.md)命令。)

如果要开始调试客户端，此命令必须适用于调试服务器中。 特定于客户端的命令，如 **.lsrcpath**，不允许。

<span id="_______-clines________lines______"></span><span id="_______-CLINES________LINES______"></span> **-clines** *lines*   
可以在远程调试过程中访问的命令历史记录中设置命令的大致的数目。 有关详细信息，以及更改此数字的其他方法，请参阅[使用调试器命令](using-debugger-commands.md)。

<span id="_______-d______"></span><span id="_______-D______"></span> **-d**   
（仅适用于内核模式）在重新启动后，调试器将中断到目标计算机加载了内核模块。 (此中断是早于从中断 **-b**选项。)请参阅[崩溃和重新启动目标计算机](crashing-and-rebooting-the-target-computer.md)为详细信息和更改此状态的其他方法。

<span id="_______-ee__masm_c___"></span><span id="_______-EE__MASM_C___"></span> **-ee** {**masm**|**c++**}  
设置默认表达式计算器。 如果**masm**指定，则将使用 MASM 表达式语法。 如果**c + +** 指定，则C++将使用表达式语法。 如果 **-ee**省略选项，MASM 表达式语法将用作默认值。 请参阅[评估表达式](evaluating-expressions.md)有关详细信息。

<span id="_______-failinc______"></span><span id="_______-FAILINC______"></span> **-failinc**   
会导致调试器忽略任何可疑的符号。 在调试用户模式或内核模式的小型转储文件时，此选项将会阻止调试器加载任何模块不能映射其映像。 有关详细信息和控制这的其他方法，请参阅[SYMOPT\_EXACT\_符号](symbol-options.md#symopt-exact-symbols)。

<span id="_______-g______"></span><span id="_______-G______"></span> **-g**   
（仅限用户模式）将忽略目标应用程序中的初始断点。 此选项将导致目标应用程序后仍继续运行已启动或 WinDbg 附加到它，除非已设置另一个断点。 请参阅[初始断点](initial-breakpoint.md)有关详细信息。

<span id="_______-G______"></span><span id="_______-g______"></span> **-G**   
（仅限用户模式）将忽略在进程终止时的最后一个断点。 通常情况下，在调试会话结束映像 run-down 过程。 此选项将导致子终止时立即结束调试会话。 这具有与输入命令相同的效果**sxd epr**。 有关详细信息，请参阅[控制异常和事件](controlling-exceptions-and-events.md)。

<span id="_______-hd______"></span><span id="_______-HD______"></span> **-hd**   
（仅限用户模式）指定不应使用调试堆。

<span id="_______-I_S_"></span><span id="_______-i_s_"></span> **-I**\[**S**\]  
将 WinDbg 作为事后调试器安装。 有关详细信息，请参阅[启用事后调试](enabling-postmortem-debugging.md)。

尝试此操作后，会显示成功或失败消息。 如果**S**是包括，执行此过程是以无提示方式是否成功; 唯一的失败消息会显示。

**-我**参数必须不能与任何其他参数。 此命令将实际上不会启动的 WinDbg 中，尽管 WinDbg 窗口可能会显示一段时间。

<span id="_______-IA_S_"></span><span id="_______-ia_s_"></span> **-IA**\[**S**\]  
将 WinDbg 文件扩展.dmp、.mdmp 和.wew 注册表中的与相关联。 尝试此操作后，会显示成功或失败消息。 如果**S**是包括，执行此过程是以无提示方式是否成功; 唯一的失败消息会显示。 进行这种关联后，双击与下列扩展名之一的文件将启动 WinDbg。

**-IA**参数必须不能与任何其他参数。 此命令将实际上不会启动的 WinDbg 中，尽管 WinDbg 窗口可能会显示一段时间。

<span id="_______-IU________KeyString______"></span><span id="_______-iu________keystring______"></span><span id="_______-IU________KEYSTRING______"></span> **-IU** *KeyString*   
将调试程序远程处理注册为 URL 类型，以便用户可以自动启动调试器远程客户端使用的 URL。 *KeyString*具有格式`remdbgeng://RemotingOption`。 *RemotingOption*是一个字符串，定义主题中定义的传输协议[**激活调试客户端**](activating-a-debugging-client.md)。 如果此操作成功，则不显示任何消息;如果失败，，显示一条错误消息。

**-IU**参数必须不能与任何其他参数。 尽管 WinDbg 窗口可能会显示一段时间，则此命令将不会实际启动 WinDbg。

<span id="_______-i_______ImagePath______"></span><span id="_______-i_______imagepath______"></span><span id="_______-I_______IMAGEPATH______"></span> **-i** *ImagePath*   
指定生成错误的可执行文件的位置。 如果路径包含空格，应括在引号中。

<span id="_______-j______"></span><span id="_______-J______"></span> **-j**   
允许日志。

<span id="_______-k__ConnectType_"></span><span id="_______-k__connecttype_"></span><span id="_______-K__CONNECTTYPE_"></span> **-k** \[*ConnectType*\]  
（仅适用于内核模式）启动调试会话的内核。 有关详细信息，请参阅[Live 内核模式调试使用 WinDbg](performing-kernel-mode-debugging-using-windbg.md)。 如果 **-k**使用不带任何*ConnectType*其后的选项，它必须是命令行上的最后一项。

<span id="_______-kl______"></span><span id="_______-KL______"></span> **-kl**   
（仅适用于内核模式）启动内核调试与调试器相同的计算机上的会话。

<span id="_______-kx_______ExdiOptions______"></span><span id="_______-kx_______exdioptions______"></span><span id="_______-KX_______EXDIOPTIONS______"></span> **-kx** *ExdiOptions*   
（仅适用于内核模式）启动调试会话使用 EXDI 驱动程序的内核。 本文档中未介绍 EXDI 驱动程序。 如果您有 EXDI 接口到硬件探测或硬件模拟器，请联系 Microsoft 获取调试信息。

<span id="_______-log_o_a__LogFile"></span><span id="_______-log_o_a__logfile"></span><span id="_______-LOG_O_A__LOGFILE"></span> **-log**{**o**|**a**} *LogFile*  
开始将信息记入日志文件。 如果指定的日志文件已存在，则将覆盖如果 **-徽标**使用。 如果**loga**是使用，输出将追加到文件。 有关更多详细信息，请参阅[的日志文件保留在 WinDbg 中](keeping-a-log-file-in-windbg.md)。

<span id="_______-lsrcpath______"></span><span id="_______-LSRCPATH______"></span> **-lsrcpath**   
为远程客户端设置的本地源路径。 此选项必须遵循 **-远程**命令行上。

<span id="_______-n______"></span><span id="_______-N______"></span> **-n**   
*干扰符号负载*:启用从符号处理程序的详细输出。 有关详细信息和控制这的其他方法，请参阅[SYMOPT\_调试](symbol-options.md#symopt-debug)。

<span id="_______-noinh______"></span><span id="_______-NOINH______"></span> **-noinh**   
（仅限用户模式）可以防止创建句柄继承从调试器调试程序的进程。 有关控制此的其他方法，请参阅[调试用户模式进程使用 WinDbg](debugging-a-user-mode-process-using-windbg.md)。

<span id="_______-noprio______"></span><span id="_______-NOPRIO______"></span> **-noprio**   
可以防止任何优先级更改。 此参数将阻止 WinDbg 让几个处于活动状态时的 CPU 时间的优先级。

<span id="_______-noshell______"></span><span id="_______-NOSHELL______"></span> **-noshell**   
禁止所有 **.shell**命令。 此禁止将持续的时间运行调试器，即使开始新的调试会话。 有关详细信息，以及禁用 shell 命令的其他方法，请参阅[使用 Shell 命令](using-shell-commands.md)。

<span id="_______-o______"></span><span id="_______-O______"></span> **-o**   
（仅限用户模式）调试启动目标应用程序 （子进程） 的所有进程。 默认情况下，创建的一个正在调试的进程将运行它们通常要做。

<span id="_______-openPrivateDumpByHandle______"></span><span id="_______-OPENPRIVATEDUMPBYHANDLE______"></span> **-openPrivateDumpByHandle** *Handle*   
指定要调试的崩溃转储文件的句柄。

<span id="_______-p_______PID______"></span><span id="_______-p_______pid______"></span><span id="_______-P_______PID______"></span> **-p** *PID*   
指定要调试的十进制进程 ID。 这用于调试已在运行的进程。

<span id="_______-pb______"></span><span id="_______-PB______"></span> **-pb**   
（仅限用户模式）防止调试器附加到目标进程时请求初始被侵入的情形。 如果应用程序已挂起，或者如果你想要避免在目标中创建被侵入的情形线程，这可以很有用。

<span id="_______-pd______"></span><span id="_______-PD______"></span> **-pd**   
（仅限用户模式）导致目标应用程序不会终止调试会话结束时。 请参阅[结束调试会话在 WinDbg 中](ending-a-debugging-session-in-windbg.md)有关详细信息。

<span id="_______-pe______"></span><span id="_______-PE______"></span> **-pe**   
（仅限用户模式）指示已在调试目标应用程序。 请参阅[重新连接到目标应用程序](reattaching-to-the-target-application.md)有关详细信息。

<span id="_______-pn_______Name______"></span><span id="_______-pn_______name______"></span><span id="_______-PN_______NAME______"></span> **-pn** *Name*   
指定要调试的进程的名称。 （此名称必须是唯一的。）这用于调试已在运行的进程。

<span id="_______-pr______"></span><span id="_______-PR______"></span> **-pr**   
（仅限用户模式）导致调试器开始运行时它将附加到它的目标进程。 如果应用程序已挂起状态，并且您不希望继续执行，这很有用。

<span id="_______-psn_______ServiceName______"></span><span id="_______-psn_______servicename______"></span><span id="_______-PSN_______SERVICENAME______"></span> **-psn** *ServiceName*   
指定要调试的过程中包含的服务的名称。 这用于调试已在运行的进程。

<span id="_______-pt_______Seconds______"></span><span id="_______-pt_______seconds______"></span><span id="_______-PT_______SECONDS______"></span> **-pt** *Seconds*   
指定中断超时，以秒为单位。 默认值为 30。 请参阅[控制目标](controlling-the-target.md)有关详细信息。

<span id="_______-pv______"></span><span id="_______-PV______"></span> **-pv**   
（仅限用户模式）指定调试器应 noninvasively 附加到目标进程。 有关详细信息，请参阅[非侵入调试 （用户模式）](noninvasive-debugging--user-mode-.md)。

<span id="_______-Q______"></span><span id="_______-q______"></span> **-Q**   
禁止显示"保存工作区？" 对话框中指定选项。 工作区不会自动保存。 请参阅[使用工作区](using-workspaces.md)有关详细信息。

<span id="_______-QS______"></span><span id="_______-qs______"></span> **-QS**   
禁止显示"重新加载源"？ 对话框中指定选项。 源文件不会自动重新加载。

<span id="_______-QSY______"></span><span id="_______-qsy______"></span> **-QSY**   
禁止显示"重新加载源"？ 对话框中，会自动重新加载源文件。

<span id="_______-QY______"></span><span id="_______-qy______"></span> **-QY**   
禁止显示"保存工作区？" 对话框和自动保存工作区。 请参阅[使用工作区](using-workspaces.md)有关详细信息。

<span id="_______-robp______"></span><span id="_______-ROBP______"></span> **-robp**   
这允许 CDB 只读内存页上设置断点。 （默认值是此类操作失败。）

<span id="_______-sdce______"></span><span id="_______-SDCE______"></span> **-sdce**   
使调试器显示**文件访问错误**符号加载过程中的消息。 有关详细信息和控制这的其他方法，请参阅[SYMOPT\_失败\_严重\_错误](symbol-options.md#symopt-fail-critical-errors)。

<span id="_______-secure______"></span><span id="_______-SECURE______"></span> **-secure**   
激活[安全模式](secure-mode.md)。

<span id="_______-ses______"></span><span id="_______-SES______"></span> **-ses**   
使调试器执行的所有符号文件严格评估，并忽略任何可疑的符号。 有关详细信息和控制这的其他方法，请参阅[SYMOPT\_EXACT\_符号](symbol-options.md#symopt-exact-symbols)。

<span id="_______-sflags_0x________Number______"></span><span id="_______-sflags_0x________number______"></span><span id="_______-SFLAGS_0X________NUMBER______"></span> **-sflags 0 x** *数*   
一次性设置所有的符号处理程序选项。 *数*应能带有前缀的十六进制数**0x** -而无需十进制**0x**允许，则允许而符号选项是二进制的标志，因此建议十六进制。 应谨慎，使用此选项，因为它将替代所有符号处理程序默认值。 有关详细信息，请参阅[设置符号选项](symbol-options.md)。

<span id="_______-sicv______"></span><span id="_______-SICV______"></span> **-sicv**   
导致要忽略 CV 记录的符号处理程序。 有关详细信息和控制这的其他方法，请参阅[SYMOPT\_忽略\_CVREC](symbol-options.md#symopt-ignore-cvrec)。

<span id="_______-sins______"></span><span id="_______-SINS______"></span> **-sins**   
会导致调试器忽略符号路径和可执行文件映像路径环境变量。 有关详细信息，请参阅[SYMOPT\_忽略\_NT\_SYMPATH](symbol-options.md#symopt-ignore-nt-sympath)。

<span id="_______-snc______"></span><span id="_______-SNC______"></span> **-snc**   
使调试器后，若要关闭C++转换。 有关详细信息和控制这的其他方法，请参阅[SYMOPT\_否\_CPP](symbol-options.md#symopt-no-cpp)。

<span id="_______-snul______"></span><span id="_______-SNUL______"></span> **-snul**   
禁用自动符号加载的非限定名称。 有关详细信息和控制这的其他方法，请参阅[SYMOPT\_否\_UNQUALIFIED\_加载](symbol-options.md#symopt-no-unqualified-loads)。

<span id="_______-srcpath_______SourcePath______"></span><span id="_______-srcpath_______sourcepath______"></span><span id="_______-SRCPATH_______SOURCEPATH______"></span> **-srcpath** *SourcePath*   
指定源文件搜索路径。 用分号分隔多个路径 (**;**)。 如果路径包含空格，应括在引号中。 有关详细信息，以及更改此路径的其他方法，请参阅[源路径](source-path.md)。

<span id="_______-sup______"></span><span id="_______-SUP______"></span> **-sup**   
导致要在每个符号搜索期间搜索公共符号表的符号处理程序。 有关详细信息和控制这的其他方法，请参阅[SYMOPT\_自动\_PUBLICS](symbol-options.md#symopt-auto-publics)。

<span id="_______-T_______Title______"></span><span id="_______-t_______title______"></span><span id="_______-T_______TITLE______"></span> **-T** *Title*   
设置 WinDbg 窗口标题。

<span id="_______-v______"></span><span id="_______-V______"></span> **-v**   
启用从调试器的详细输出。

<span id="_______-W_______Workspace______"></span><span id="_______-w_______workspace______"></span><span id="_______-W_______WORKSPACE______"></span> **-W** *Workspace*   
加载给定的命名工作区。 如果工作区名称包含空格，请将其括在引号中。 如果不存在此名称的任何工作区，将为您提供具有此名称创建新的工作区或放弃加载尝试的选项。 有关详细信息，请参阅[使用工作区](using-workspaces.md)。

<span id="_______-WF_______Filename______"></span><span id="_______-wf_______filename______"></span><span id="_______-WF_______FILENAME______"></span> **-WF** *Filename*   
从给定的文件加载工作区。 *文件名*应包括文件和扩展 (通常.wew)。 如果工作区名称包含空格，请将其括在引号中。 如果存在具有此名称没有工作区文件，将为您提供具有此名称创建一个新的工作区文件或放弃加载尝试的选项。 有关详细信息，请参阅[使用工作区](using-workspaces.md)。

<span id="_______-WX______"></span><span id="_______-wx______"></span> **-WX**   
禁用自动工作区中加载。 有关详细信息，请参阅[使用工作区](using-workspaces.md)。

<span id="_______-y_______SymbolPath______"></span><span id="_______-y_______symbolpath______"></span><span id="_______-Y_______SYMBOLPATH______"></span> **-y** *SymbolPath*   
指定符号搜索路径。 用分号分隔多个路径 (**;**)。 如果路径包含空格，应括在引号中。 有关详细信息，以及更改此路径的其他方法，请参阅[符号路径](symbol-path.md)。

<span id="_______-z_______DumpFile______"></span><span id="_______-z_______dumpfile______"></span><span id="_______-Z_______DUMPFILE______"></span> **-z** *DumpFile*   
指定要调试的崩溃转储文件的名称。 如果路径和文件名称包含空格，这必须用引号括起来。 可以通过包含多个同时打开多个转储文件**z**选项，每个后跟一个不同*DumpFile*值。 有关详细信息，请参阅[分析用户模式转储文件](analyzing-a-user-mode-dump-file.md)或[分析具有 WinDbg 的内核模式转储文件](analyzing-a-kernel-mode-dump-file-with-windbg.md)。

<span id="_______-zp_______PageFile______"></span><span id="_______-zp_______pagefile______"></span><span id="_______-ZP_______PAGEFILE______"></span> **-zp** *PageFile*   
指定修改的页面文件的名称。 如果您正在调试转储文件，并且想要使用，这很有用[ **.pagein （内存中的页）** ](-pagein--page-in-memory-.md)命令。 不能使用 **-zp**与标准的 Windows 页文件--可以使用仅专门修改页面文件。

<span id="_______executable______"></span><span id="_______EXECUTABLE______"></span> *executable*   
指定可执行进程的命令行。 这用于启动新进程，并对其进行调试。 这必须是命令行上的最后一个项目。 可执行文件的名称传递给可执行文件作为其参数字符串后的所有文本。 有关详细信息，请参阅[调试用户模式进程使用 WinDbg](debugging-a-user-mode-process-using-windbg.md)。

<span id="_______-_______"></span> **-?**   
此 HTML 帮助窗口将弹出。

当从命令行运行调试器时，指定目标应用程序后应用程序的文件名称的参数。 例如：

```dbgcmd
windbg myexe arg1 arg2
```

 

 





