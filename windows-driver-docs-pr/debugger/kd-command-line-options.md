---
title: KD 命令行选项
description: KD 的第一次用户应该以调试使用 KD 和 NTKD 部分开头。
ms.assetid: 76c11b45-8469-4f27-840d-06477d8922b8
keywords:
- KD 命令行选项 Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- KD Command-Line Options
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 30c2ec62ee88c9ae1bfe68388bf9e15016f6fc16
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367220"
---
# <a name="kd-command-line-options"></a>KD 命令行选项


KD 的第一次用户应开头[调试使用 KD 和 NTKD](debugging-using-kd-and-ntkd.md)部分。

KD 命令行使用以下语法。

```dbgcmd
kd [ -server ServerTransport | -remote ClientTransport ] 
   [-b | -x] [-d] [-bonc] [-m] [-myob] [-lines] [-n] [-r] [-s] 
   [-v] [-clines lines] [-failinc] [-noio] [-noshell] 
   [-secure] [-sdce] [-ses] [-sicv] [-sins] [-snc] [-snul]
   [-sup] [-sflags 0xNumber] [-log{a|au|o|ou} LogFile] 
   [-aExtension] [-zp PageFile] 
   [-i ImagePath] [-y SymbolPath]  [-srcpath SourcePath] 
   [-k ConnectType | -kl | -kqm | -kx ExdiOptions] [-ee {masm|c++}] 
   [-z DumpFile] [-cf "filename"] [-cfr "filename"] [-c "command"] 
   [-t PrintErrorLevel] [-version] 

kd -iu KeyString

kd -QR Server 

kd -wake PID 

kd -?
```

按照 KD 命令行选项的说明。 仅**的远程**并 **-server**选项是区分大小写。 可以使用正斜杠 （/） 替换初始的连字符。 可以连接选项，这不需要的额外参数-因此**kd-r-n v**可以将其写作**kd rnv**。

如果**的远程**或 **-server**选项，则它必须出现在之前在命令行上的任何其他选项。

## <a name="span-idddkkdcommandlineoptionsdbgspanspan-idddkkdcommandlineoptionsdbgspanparameters"></a><span id="ddk_kd_command_line_options_dbg"></span><span id="DDK_KD_COMMAND_LINE_OPTIONS_DBG"></span>参数


<span id="_______-server_______ServerTransport______"></span><span id="_______-server_______servertransport______"></span><span id="_______-SERVER_______SERVERTRANSPORT______"></span> **-server** *ServerTransport*   
创建可由其他调试器的调试服务器。 有关可能的说明*服务器传送*，请参阅[**激活调试服务器**](activating-a-debugging-server.md)。 如果使用此参数，它必须是命令行中的第一个参数。

<span id="_______-remote_______ClientTransport______"></span><span id="_______-remote_______clienttransport______"></span><span id="_______-REMOTE_______CLIENTTRANSPORT______"></span> **-remote** *ClientTransport*   
创建调试客户端，并连接到已在运行的调试服务器。 有关可能的说明*ClientTransport*值，请参阅[**激活调试客户端**](activating-a-debugging-client.md)。 如果使用此参数，它必须是命令行中的第一个参数。

<span id="_______-a________Extension______"></span><span id="_______-a________extension______"></span><span id="_______-A________EXTENSION______"></span> **-a** *扩展*   
设置默认扩展插件 DLL。 默认值为 kdextx86.dll 或 kdexts.dll。 必须有后的没有空格不能包含"a"、 和.dll 文件扩展名。 有关详细信息，并设置此默认设置的其他方法，请参阅[加载的调试器扩展 Dll](loading-debugger-extension-dlls.md)。

<span id="_______-b______"></span><span id="_______-B______"></span> **-b**   
不再支持此选项。

<span id="_______-bonc______"></span><span id="_______-BONC______"></span> **-bonc**   
如果指定此选项，则调试器将在会话开始时立即中断到目标。 连接到可能不当前分解为目标的调试服务器时，这是特别有用。

<span id="_______-c__command_______"></span><span id="_______-C__COMMAND_______"></span> **-c "** <em>command</em> **"**    
指定要在启动时运行的初始调试器命令。 此命令必须用引号括起来。 可以用分号分隔多个命令。 (如果有很长的命令列表，可能会更容易将其放在一个脚本，然后使用 **-c**选项与[  **$ &lt;，$&gt;&lt;，$&gt; &lt;，$$&gt; &lt; （运行脚本文件）** ](-----------------------a---run-script-file-.md)命令。)

如果要开始调试客户端，此命令必须适用于调试服务器中。 特定于客户端的命令，如 **.lsrcpath**，不允许。

<span id="_______-cf__filename_______"></span><span id="_______-CF__FILENAME_______"></span> **-cf "** <em>filename</em> **"**    
指定的路径和脚本文件的名称。 启动调试器时，就立即执行此脚本文件。 如果*文件名*包含的空格，则必须用引号引起来。 如果省略路径，则假定当前目录。 如果不使用-cf 选项，则在当前目录中的文件 ntsd.ini 用作脚本文件。 如果该文件不存在，会发生任何错误。 有关详细信息，请参阅[使用脚本文件](using-script-files.md)。

<span id="_______-cfr__filename_______"></span><span id="_______-CFR__FILENAME_______"></span> **-cfr "** <em>filename</em> **"**    
指定的路径和脚本文件的名称。 在启动调试器，并随时重新启动目标执行此脚本文件。 如果*文件名*包含的空格，则必须用引号引起来。 如果省略路径，则假定当前目录。 如果该文件不存在，会发生任何错误。 有关详细信息，请参阅[使用脚本文件](using-script-files.md)。

<span id="_______-clines________lines______"></span><span id="_______-CLINES________LINES______"></span> **-clines** *lines*   
可以在远程调试过程中访问的命令历史记录中设置命令的大致的数目。 有关详细信息，以及更改此数字的其他方法，请参阅[使用调试器命令](using-debugger-commands.md)。

<span id="_______-d______"></span><span id="_______-D______"></span> **-d**   
在重新启动后，调试器将中断到目标计算机加载了内核模块。 (此中断是早于从中断 **-b**选项。)请参阅[崩溃和重新启动目标计算机](crashing-and-rebooting-the-target-computer.md)为详细信息和更改此状态的其他方法。

<span id="_______-ee__masm_c___"></span><span id="_______-EE__MASM_C___"></span> **-ee** {**masm**|**c++** }  
设置默认表达式计算器。 如果**masm**指定，则将使用 MASM 表达式语法。 如果**c + +** 指定，则C++将使用表达式语法。 如果 **-ee**省略选项，MASM 表达式语法将用作默认值。 请参阅[评估表达式](evaluating-expressions.md)有关详细信息。

<span id="_______-failinc______"></span><span id="_______-FAILINC______"></span> **-failinc**   
会导致调试器忽略任何可疑的符号。 在调试用户模式或内核模式的小型转储文件时，此选项将会阻止调试器加载任何模块不能映射其映像。 有关详细信息和控制这的其他方法，请参阅[SYMOPT\_EXACT\_符号](symbol-options.md#symopt-exact-symbols)。

<span id="_______-i_______ImagePath______"></span><span id="_______-i_______imagepath______"></span><span id="_______-I_______IMAGEPATH______"></span> **-i** *ImagePath*   
指定生成错误的可执行文件的位置。 如果路径包含空格，应括在引号中。

<span id="_______-iu________KeyString______"></span><span id="_______-iu________keystring______"></span><span id="_______-IU________KEYSTRING______"></span> **-iu** *KeyString*   
将调试程序远程处理注册为 URL 类型，以便用户可以自动启动调试器远程客户端使用的 URL。 *KeyString*具有格式`remdbgeng://RemotingOption`。 *RemotingOption*是一个字符串，定义主题中定义的传输协议[**激活调试客户端**](activating-a-debugging-client.md)。 如果此操作成功，则不显示任何消息;如果失败，，显示一条错误消息。

**-Iu**参数必须不能与任何其他参数。 此命令将实际上不会启动 KD。

<span id="_______-k_______ConnectType______"></span><span id="_______-k_______connecttype______"></span><span id="_______-K_______CONNECTTYPE______"></span> **-k** *ConnectType*   
告知调试器如何连接到的目标。 有关详细信息，请参阅[调试使用 KD 和 NTKD](debugging-using-kd-and-ntkd.md)。

<span id="_______-kl______"></span><span id="_______-KL______"></span> **-kl**   
启动内核调试与调试器相同的计算机上的会话。

<span id="_______-kqm______"></span><span id="_______-KQM______"></span> **-kqm**   
在静默模式下启动 KD。

<span id="_______-kx_______ExdiOptions______"></span><span id="_______-kx_______exdioptions______"></span><span id="_______-KX_______EXDIOPTIONS______"></span> **-kx** *ExdiOptions*   
启动调试会话使用 EXDI 驱动程序的内核。 本文档中未介绍 EXDI 驱动程序。 如果您有 EXDI 接口到硬件探测或硬件模拟器，请联系 Microsoft 获取调试信息。

<span id="_______-lines______"></span><span id="_______-LINES______"></span> **-lines**   
启用源行调试。 如果省略此选项，则[ **.lines （切换源行支持）** ](-lines--toggle-source-line-support-.md)命令将需要使用之前将允许源调试。 有关控制此的其他方法，请参阅[SYMOPT\_负载\_行](symbol-options.md#symopt-load-lines)。

<span id="_______-log_a_au_o_ou__LogFile"></span><span id="_______-log_a_au_o_ou__logfile"></span><span id="_______-LOG_A_AU_O_OU__LOGFILE"></span> **-log**{**a|au|o|ou**} *LogFile*  
开始将信息记入日志文件。 如果*日志文件*已存在，如果将覆盖 **-徽标**使用时，或输出将追加到文件，如果 **-loga**使用。 **-Logau**并 **-logou**选项作用类似于 **-loga**并 **-徽标**分别，除非日志文件是 Unicode 文件。 有关更多详细信息，请参阅[的日志文件保留 KD](keeping-a-log-file-in-kd.md)。

<span id="_______-m______"></span><span id="_______-M______"></span> **-m**   
指示串行端口已连接到调制解调器。 指示调试器要监视的载波检测信号。

<span id="_______-myob______"></span><span id="_______-MYOB______"></span> **-myob**   
如果没有与 dbghelp.dll 版本不匹配，则调试器将继续运行。 (无需 **-myob**开关，这被认为是致命错误。)

此选项产生的副作用是，禁止显示分解为目标计算机时通常会显示警告。

<span id="_______-n______"></span><span id="_______-N______"></span> **-n**   
*干扰符号负载*:启用从符号处理程序的详细输出。 有关详细信息和控制这的其他方法，请参阅[SYMOPT\_调试](symbol-options.md#symopt-debug)。

<span id="_______-noio______"></span><span id="_______-NOIO______"></span> **-noio**   
防止调试服务器正用于输入或输出。 输入将仅接受来自调试客户端 (以及任何初始命令或由指定的命令脚本 **-c**命令行选项)。

所有输出会都定向到调试客户端。 有关更多详细信息，请参阅[**激活调试服务器**](activating-a-debugging-server.md)。

<span id="_______-noshell______"></span><span id="_______-NOSHELL______"></span> **-noshell**   
禁止所有 **.shell**命令。 此禁止将持续的时间运行调试器，即使开始新的调试会话。 有关详细信息，以及禁用 shell 命令的其他方法，请参阅[使用 Shell 命令](using-shell-commands.md)。

<span id="_______-QR_______Server______"></span><span id="_______-qr_______server______"></span><span id="_______-QR_______SERVER______"></span> **-QR** *Server*   
列出在指定的网络服务器上运行的所有调试服务器。 双反斜杠 ( **\\\\** ) 前面*Server*是可选的。 请参阅[**搜索调试服务器**](searching-for-debugging-servers.md)有关详细信息。

**-QR**参数必须不能与任何其他参数。 此命令将实际上不会启动 KD。

<span id="_______-r______"></span><span id="_______-R______"></span> **-r**   
显示寄存器信息。

<span id="_______-s______"></span><span id="_______-S______"></span> **-s**   
禁用延迟符号加载。 这将减慢进程启动。 有关详细信息和控制这的其他方法，请参阅[SYMOPT\_延期\_加载](symbol-options.md#symopt-deferred-loads)。

<span id="_______-sdce______"></span><span id="_______-SDCE______"></span> **-sdce**   
使调试器显示**文件访问错误**符号加载过程中的对话框。 有关详细信息和控制这的其他方法，请参阅[SYMOPT\_失败\_严重\_错误](symbol-options.md#symopt-fail-critical-errors)。

<span id="_______-secure______"></span><span id="_______-SECURE______"></span> **-secure**   
激活[安全模式](secure-mode.md)。

<span id="_______-ses______"></span><span id="_______-SES______"></span> **-ses**   
使调试器执行的所有符号文件严格评估，并忽略任何可疑的符号。 有关详细信息和控制这的其他方法，请参阅[SYMOPT\_EXACT\_符号](symbol-options.md#symopt-exact-symbols)。

<span id="_______-sflags_0xNumber"></span><span id="_______-sflags_0xnumber"></span><span id="_______-SFLAGS_0XNUMBER"></span> * *-sflags 0 x * * * 数*  
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
指定源文件搜索路径。 用分号分隔多个路径 ( **;** )。 如果路径包含空格，应括在引号中。 有关详细信息，以及更改此路径的其他方法，请参阅[源路径](source-path.md)。

<span id="_______-sup______"></span><span id="_______-SUP______"></span> **-sup**   
导致要在每个符号搜索期间搜索公共符号表的符号处理程序。 有关详细信息和控制这的其他方法，请参阅[SYMOPT\_自动\_PUBLICS](symbol-options.md#symopt-auto-publics)。

<span id="_______-t________PrintErrorLevel______"></span><span id="_______-t________printerrorlevel______"></span><span id="_______-T________PRINTERRORLEVEL______"></span> **-t** *PrintErrorLevel*   
指定将导致调试程序来显示一条错误消息的错误级别。 这是一个十进制数等于 0、 1、 2 或 3。 按如下所示了该选项值：

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ReplTest1</th>
<th align="left">Constant</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>NONE</p></td>
<td align="left"><p>不显示任何错误。</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>错误</p></td>
<td align="left"><p>显示错误级别的调试事件。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>2</p></td>
<td align="left"><p>MINORERROR</p></td>
<td align="left"><p>显示 MINORERROR 和错误级别的调试事件。</p></td>
</tr>
<tr class="even">
<td align="left"><p>3</p></td>
<td align="left"><p>警告</p></td>
<td align="left"><p>显示警告，MINORERROR 和错误级别的调试事件。</p></td>
</tr>
</tbody>
</table>

 

此错误级别仅在已检查版本的 Microsoft Windows 中具有含义。 默认值为 1。

<span id="_______-v______"></span><span id="_______-V______"></span> **-v**   
生成负载，延迟加载的详细消息，并卸载。

<span id="_______-version______"></span><span id="_______-VERSION______"></span> **-version**   
打印的调试器版本字符串。

<span id="_______-wake_______PID______"></span><span id="_______-wake_______pid______"></span><span id="_______-WAKE_______PID______"></span> **-wake** *PID*   
原因睡眠模式下，若要通过指定其进程 ID 的用户模式下调试程序结束*PID*。 在睡眠模式期间，必须在目标计算机上发出此命令。 请参阅[控制用户模式下调试程序与内核调试程序](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)有关详细信息。

**-唤醒**参数必须不能与任何其他参数。 此命令将实际上不会启动 KD。

<span id="_______-x______"></span><span id="_______-X______"></span> **-x**   
使调试器时首次出现异常，而不是让应用程序或模块引发异常的异常处理中断。 (与相同 **-b**，除了初始**eb nt ！NtGlobalFlag 9; g**命令。)

<span id="_______-y_______SymbolPath______"></span><span id="_______-y_______symbolpath______"></span><span id="_______-Y_______SYMBOLPATH______"></span> **-y** *SymbolPath*   
指定符号搜索路径。 用分号分隔多个路径 ( **;** )。 如果路径包含空格，应括在引号中。 有关详细信息，以及更改此路径的其他方法，请参阅[符号路径](symbol-path.md)。

<span id="_______-z_______DumpFile______"></span><span id="_______-z_______dumpfile______"></span><span id="_______-Z_______DUMPFILE______"></span> **-z** *DumpFile*   
指定要调试的崩溃转储文件的名称。 如果路径和文件名称包含空格，这必须用引号括起来。 可以通过包含多个同时打开多个转储文件**z**选项，每个后跟一个不同*DumpFile*值。 有关详细信息，请参阅[分析 KD 具有的内核模式转储文件](analyzing-a-kernel-mode-dump-file-with-kd.md)。

<span id="_______-zp_______PageFile______"></span><span id="_______-zp_______pagefile______"></span><span id="_______-ZP_______PAGEFILE______"></span> **-zp** *PageFile*   
指定修改的页面文件的名称。 如果您正在调试转储文件，并且想要使用，这很有用[ **.pagein （内存中的页）** ](-pagein--page-in-memory-.md)命令。 不能使用 **-zp**与标准的 Windows 页面文件，可以使用只有专门修改页面文件。

<span id="_______-_______"></span> **-?**    
显示命令行帮助文本。

KD 会自动检测目标运行时所在的平台。 不需要 KD 命令行上指定目标。 较早的语法 (使用名称*I386KD*或*IA64KD*) 已过时。

 

 





