---
title: KD 命令行选项
description: 首次使用 KD 时，应使用 KD 和 NTKD 部分的调试开始。
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
ms.openlocfilehash: ccaaaa3dfd5918262df6410ff966c8579214d1f7
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75209835"
---
# <a name="kd-command-line-options"></a>KD 命令行选项


首次使用 KD 时，应[使用 KD 和 NTKD](debugging-using-kd-and-ntkd.md)部分的调试开始。

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

KD 命令行选项的说明如下。 只有 **-remote**和 **-server**选项区分大小写。 可以使用正斜杠（/）替换初始连字符。 可以连接不采用任何其他参数的选项--因此， **kd**可以编写为**kd-rnv**。

如果使用了 **-remote**或 **-server**选项，则它必须出现在命令行上的任何其他选项之前。

## <a name="span-idddk_kd_command_line_options_dbgspanspan-idddk_kd_command_line_options_dbgspanparameters"></a><span id="ddk_kd_command_line_options_dbg"></span><span id="DDK_KD_COMMAND_LINE_OPTIONS_DBG"></span>Parameters


<span id="_______-server_______ServerTransport______"></span><span id="_______-server_______servertransport______"></span><span id="_______-SERVER_______SERVERTRANSPORT______"></span>**-server** *ServerTransport*   
创建可由其他调试器访问的调试服务器。 有关可能的*ServerTransport*的说明，请参阅[**激活调试服务器**](activating-a-debugging-server.md)。 使用此参数时，该参数必须是命令行中的第一个参数。

<span id="_______-remote_______ClientTransport______"></span><span id="_______-remote_______clienttransport______"></span><span id="_______-REMOTE_______CLIENTTRANSPORT______"></span>**-remote** *ClientTransport*   
创建调试客户端，并连接到已在运行的调试服务器。 有关可能的*ClientTransport*值的说明，请参阅[**激活调试客户端**](activating-a-debugging-client.md)。 使用此参数时，该参数必须是命令行中的第一个参数。

<span id="_______-a________Extension______"></span><span id="_______-a________extension______"></span><span id="_______-A________EXTENSION______"></span>**-** *扩展*   
设置默认扩展 DLL。 默认值为 kdextx86 或 kdexts。 "A" 后面一定不能有空格，并且不得包含 .dll 文件扩展名。 有关详细信息和设置此默认设置的其他方法，请参阅[加载调试器扩展 dll](loading-debugger-extension-dlls.md)。

<span id="_______-b______"></span><span id="_______-B______"></span>**-b**   
不再支持此选项。

<span id="_______-bonc______"></span><span id="_______-BONC______"></span>**-bonc**   
如果指定此选项，则调试器将在会话开始时立即进入目标。 这在连接到可能当前未分解到目标的调试服务器时特别有用。

<span id="_______-c__command_______"></span><span id="_______-C__COMMAND_______"></span>**-c "**<em>command</em>**"**   
指定要在启动时运行的初始调试器命令。 此命令必须用引号引起来。 可以用分号分隔多个命令。 （如果您有一个长命令列表，则可以更容易地将其放入脚本，然后将 **-c**选项与[**$&lt;，$&gt;&lt;，$&gt;&lt;，$ $&gt;&lt; （运行脚本文件）**](-----------------------a---run-script-file-.md)命令一起使用。）

如果要启动调试客户端，则必须将此命令用于调试服务器。 不允许使用客户端特定的命令（如**lsrcpath**）。

<span id="_______-cf__filename_______"></span><span id="_______-CF__FILENAME_______"></span>**-cf "**<em>filename</em>**"**   
指定脚本文件的路径和名称。 启动调试器后，将立即执行该脚本文件。 如果*filename*包含空格，则必须用引号将其引起来。 如果省略该路径，则假定为当前目录。 如果未使用-cf 选项，则使用当前目录中的文件 ntsd 作为脚本文件。 如果文件不存在，则不会发生错误。 有关详细信息，请参阅[使用脚本文件](using-script-files.md)。

<span id="_______-cfr__filename_______"></span><span id="_______-CFR__FILENAME_______"></span>**-cfr "**<em>filename</em>**"**   
指定脚本文件的路径和名称。 一旦启动调试器，就会执行该脚本文件，并在每次重新启动目标时执行。 如果*filename*包含空格，则必须用引号将其引起来。 如果省略该路径，则假定为当前目录。 如果文件不存在，则不会发生错误。 有关详细信息，请参阅[使用脚本文件](using-script-files.md)。

<span id="_______-clines________lines______"></span><span id="_______-CLINES________LINES______"></span>**-clines** *行*   
设置在远程调试过程中可以访问的命令历史记录中的大概命令数。 有关详细信息以及其他更改此数字的方法，请参阅[使用调试器命令](using-debugger-commands.md)。

<span id="_______-d______"></span><span id="_______-D______"></span>**-d**   
重新启动后，只要加载内核模块，调试器就会进入目标计算机。 （此中断早于 **-b**选项的 break。）有关详细信息和其他更改此状态的方法，请参阅[崩溃并重新启动目标计算机](crashing-and-rebooting-the-target-computer.md)。

<span id="_______-ee__masm_c___"></span><span id="_______-EE__MASM_C___"></span>**-ee** {**masm**|**c + +**}  
设置默认表达式计算器。 如果指定了**masm** ，将使用 masm 表达式语法。 如果指定**c + +** ， C++则使用 expression 语法。 如果省略 **-ee**选项，则将使用 MASM 表达式语法作为默认值。 有关详细信息，请参阅[计算表达式](evaluating-expressions.md)。

<span id="_______-failinc______"></span><span id="_______-FAILINC______"></span>**-failinc**   
导致调试器忽略任何有问题的符号。 调试用户模式或内核模式小型转储文件时，此选项还会阻止调试器加载其图像无法映射的任何模块。 有关详细信息和控制此方法的其他方法，请参阅[SYMOPT\_精确\_符号](symbol-options.md#symopt-exact-symbols)。

<span id="_______-i_______ImagePath______"></span><span id="_______-i_______imagepath______"></span><span id="_______-I_______IMAGEPATH______"></span>**-i** *ImagePath*   
指定生成错误的可执行文件的位置。 如果路径包含空格，则应该用引号将其引起来。

<span id="_______-iu________KeyString______"></span><span id="_______-iu________keystring______"></span><span id="_______-IU________KEYSTRING______"></span>**-iu** *KeyString*   
将调试器远程处理注册为 URL 类型，以便用户可以使用 URL 自动启动调试器远程客户端。 *KeyString*的格式 `remdbgeng://RemotingOption`。 *RemotingOption*是一个字符串，它定义在[**激活调试客户端**](activating-a-debugging-client.md)主题中定义的传输协议。 如果此操作成功，则不会显示任何消息;如果失败，将显示一条错误消息。

**-Iu**参数不得与任何其他参数一起使用。 此命令实际上不会启动 KD。

<span id="_______-k_______ConnectType______"></span><span id="_______-k_______connecttype______"></span><span id="_______-K_______CONNECTTYPE______"></span>**-k** *ConnectType*   
告诉调试器如何连接到目标。 有关详细信息，请参阅[使用 KD 和 NTKD 进行调试](debugging-using-kd-and-ntkd.md)。

<span id="_______-kl______"></span><span id="_______-KL______"></span>**-kl**   
在调试器所在的同一台计算机上启动内核调试会话。

<span id="_______-kqm______"></span><span id="_______-KQM______"></span>**-kqm**   
在安静模式下启动 KD。

<span id="_______-kx_______ExdiOptions______"></span><span id="_______-kx_______exdioptions______"></span><span id="_______-KX_______EXDIOPTIONS______"></span>**-kx** *ExdiOptions*   
使用 EXDI 驱动程序启动内核调试会话。 本文档未介绍 EXDI 驱动程序。 如果你的硬件探测或硬件模拟器具有 EXDI 接口，请联系 Microsoft 以获取调试信息。

<span id="_______-lines______"></span><span id="_______-LINES______"></span>**-行**   
启用源代码行调试。 如果省略此选项，则在允许进行源调试之前，必须使用 "[**行（切换源代码行支持）**](-lines--toggle-source-line-support-.md) " 命令。 有关控制此情况的其他方法，请参阅[SYMOPT\_LOAD\_行](symbol-options.md#symopt-load-lines)。

<span id="_______-log_a_au_o_ou__LogFile"></span><span id="_______-log_a_au_o_ou__logfile"></span><span id="_______-LOG_A_AU_O_OU__LOGFILE"></span>**-log**{**a | au | o | ou**}*日志文件*  
开始将信息记录到日志文件。 如果*日志文件*已存在，则会在使用 **-徽标**时被覆盖，否则，如果使用 **-loga** ，则输出将追加到该文件。 **-Logau**和 **-logou**选项分别与 **-loga**和 **-徽标**分别操作，只不过日志文件是 Unicode 文件。 有关更多详细信息，请参阅[在 KD 中保留日志文件](keeping-a-log-file-in-kd.md)。

<span id="_______-m______"></span><span id="_______-M______"></span>**-m**   
指示串行端口已连接到调制解调器。 指示调试器监视运营商检测信号。

<span id="_______-myob______"></span><span id="_______-MYOB______"></span>**-myob**   
如果版本与 dbghelp.dll 不匹配，则调试器将继续运行。 （如果没有 **-myob**开关，此错误将被视为错误。）

此选项的辅助效果是取消进入目标计算机时正常显示的警告。

<span id="_______-n______"></span><span id="_______-N______"></span>**-n**   
*干扰符号加载*：从符号处理程序启用详细输出。 有关详细信息和控制此方法的其他方法，请参阅[SYMOPT\_调试](symbol-options.md#symopt-debug)。

<span id="_______-noio______"></span><span id="_______-NOIO______"></span>**-noio**   
阻止调试服务器用于输入或输出。 仅从调试客户端（以及由 **-c**命令行选项指定的任何初始命令或命令脚本）接受输入。

所有输出都将定向到调试客户端。 有关更多详细信息，请参阅[**激活调试服务器**](activating-a-debugging-server.md)。

<span id="_______-noshell______"></span><span id="_______-NOSHELL______"></span>**-noshell**   
禁止全部**shell**命令。 即使启动了新的调试会话，此禁止仍将在调试器运行的时间结束。 有关详细信息，以及其他禁用 shell 命令的方法，请参阅[使用 Shell 命令](using-shell-commands.md)。

<span id="_______-QR_______Server______"></span><span id="_______-qr_______server______"></span><span id="_______-QR_______SERVER______"></span>**-QR** *服务器*   
列出在指定的网络服务器上运行的所有调试服务器。 *服务器*上的双反斜杠（**\\\\**）是可选的。 有关详细信息，请参阅[**搜索调试服务器**](searching-for-debugging-servers.md)。

**-QR**参数不得与任何其他参数一起使用。 此命令实际上不会启动 KD。

<span id="_______-r______"></span><span id="_______-R______"></span>**-r**   
显示寄存器。

<span id="_______-s______"></span><span id="_______-S______"></span>**-s**   
禁用延迟符号加载。 这会降低进程启动的速度。 有关详细信息和控制此方法的其他方法，请参阅[SYMOPT\_延迟\_负载](symbol-options.md#symopt-deferred-loads)。

<span id="_______-sdce______"></span><span id="_______-SDCE______"></span>**-sdce**   
使调试器在符号加载过程中显示**文件访问错误**对话框。 有关详细信息，请参阅[SYMOPT\_失败\_严重\_错误](symbol-options.md#symopt-fail-critical-errors)。

<span id="_______-secure______"></span><span id="_______-SECURE______"></span>**-secure**   
激活[安全模式](secure-mode.md)。

<span id="_______-ses______"></span><span id="_______-SES______"></span>**-ses**   
使调试器对所有符号文件执行严格的评估，并忽略任何有问题的符号。 有关详细信息和控制此方法的其他方法，请参阅[SYMOPT\_精确\_符号](symbol-options.md#symopt-exact-symbols)。

<span id="_______-sflags_0xNumber"></span><span id="_______-sflags_0xnumber"></span><span id="_______-SFLAGS_0XNUMBER"></span> **-sflags 0x * * * Number*  
同时设置所有符号处理程序选项。 *Number*应为以**0x**开头的十六进制数字，不允许使用**0x** ，但符号选项是二进制标志，因此建议使用十六进制。 应谨慎使用此选项，因为它将覆盖所有符号处理程序默认值。 有关详细信息，请参阅[设置符号选项](symbol-options.md)。

<span id="_______-sicv______"></span><span id="_______-SICV______"></span>**-sicv**   
导致符号处理程序忽略 CV 记录。 有关详细信息和控制此方法的其他方法，请参阅[SYMOPT\_IGNORE\_CVREC](symbol-options.md#symopt-ignore-cvrec)。

<span id="_______-sins______"></span><span id="_______-SINS______"></span>**-问题**   
导致调试器忽略符号路径和可执行图像路径环境变量。 有关详细信息，请参阅[SYMOPT\_IGNORE\_NT\_SYMPATH](symbol-options.md#symopt-ignore-nt-sympath)。

<span id="_______-snc______"></span><span id="_______-SNC______"></span>**-snc**   
使调试器关闭C++转换。 有关详细信息和控制此方法的其他方法，请参阅[SYMOPT\_no\_CPP](symbol-options.md#symopt-no-cpp)。

<span id="_______-snul______"></span><span id="_______-SNUL______"></span>**-snul**   
为非限定名称禁用自动符号加载。 有关详细信息和控制此方法的其他方法，请参阅[SYMOPT\_未\_未限定的\_负载](symbol-options.md#symopt-no-unqualified-loads)。

<span id="_______-srcpath_______SourcePath______"></span><span id="_______-srcpath_______sourcepath______"></span><span id="_______-SRCPATH_______SOURCEPATH______"></span>**-srcpath** *SourcePath*   
指定源文件搜索路径。 使用分号（**;**）分隔多个路径。 如果路径包含空格，则应该用引号将其引起来。 有关详细信息，请参阅[源路径](source-path.md)。

<span id="_______-sup______"></span><span id="_______-SUP______"></span>**-sup**   
使符号处理程序在每个符号搜索过程中搜索公共符号表。 有关详细信息和控制此方法的其他方法，请参阅[SYMOPT\_AUTO\_PUBLICS](symbol-options.md#symopt-auto-publics)。

<span id="_______-t________PrintErrorLevel______"></span><span id="_______-t________printerrorlevel______"></span><span id="_______-T________PRINTERRORLEVEL______"></span>**-t** *PrintErrorLevel*   
指定将导致调试器显示错误消息的错误级别。 这是一个十进制数，等于0、1、2或3。 这些值如下所述：

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Value</th>
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
<td align="left"><p>显示错误级别调试事件。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>2</p></td>
<td align="left"><p>MINORERROR</p></td>
<td align="left"><p>显示 MINORERROR 和错误级别调试事件。</p></td>
</tr>
<tr class="even">
<td align="left"><p>3</p></td>
<td align="left"><p>警告</p></td>
<td align="left"><p>显示警告、MINORERROR 和错误级别调试事件。</p></td>
</tr>
</tbody>
</table>

 

此错误级别仅在已检查的 Microsoft Windows 版本中具有意义。 默认值为 1。 在 Windows 10 版本1803之前，已检查的生成在较早版本的 Windows 上可用。

<span id="_______-v______"></span><span id="_______-V______"></span>**-v**   
为加载、延迟加载和卸载生成详细消息。

<span id="_______-version______"></span><span id="_______-VERSION______"></span>**-版本**   
打印调试器版本字符串。

<span id="_______-wake_______PID______"></span><span id="_______-wake_______pid______"></span><span id="_______-WAKE_______PID______"></span>**-唤醒** *PID*   
使睡眠模式对于其进程 ID 由*PID*指定的用户模式调试器结束。 在睡眠模式下，必须在目标计算机上发出此命令。 有关详细信息，请参阅[从内核调试器控制用户模式调试器](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)。

**-唤醒**参数不得与任何其他参数一起使用。 此命令实际上不会启动 KD。

<span id="_______-x______"></span><span id="_______-X______"></span>**-x**   
导致调试器在第一次发生异常时中断，而不是让引发异常的应用程序或模块进行处理。 （与 **-b**相同，但初始**eb nt 除外！NtGlobalFlag 9; g**命令。）

<span id="_______-y_______SymbolPath______"></span><span id="_______-y_______symbolpath______"></span><span id="_______-Y_______SYMBOLPATH______"></span>**-y** *SymbolPath*   
指定符号搜索路径。 使用分号（**;**）分隔多个路径。 如果路径包含空格，则应该用引号将其引起来。 有关详细信息和更改此路径的其他方式，请参阅[符号路径](symbol-path.md)。

<span id="_______-z_______DumpFile______"></span><span id="_______-z_______dumpfile______"></span><span id="_______-Z_______DUMPFILE______"></span>**-z** *DumpFile*   
指定要调试的故障转储文件的名称。 如果路径和文件名包含空格，则必须用引号将其引起来。 可以通过包含多个**z**选项来一次打开多个转储文件，每个转储文件后跟不同的*DumpFile*值。 有关详细信息，请参阅[使用 KD 分析内核模式转储文件](analyzing-a-kernel-mode-dump-file-with-kd.md)。

<span id="_______-zp_______PageFile______"></span><span id="_______-zp_______pagefile______"></span><span id="_______-ZP_______PAGEFILE______"></span>**-zp** *页面文件*   
指定已修改的页面文件的名称。 如果正在调试转储文件，并且想要使用[**pagein （内存中的页）**](-pagein--page-in-memory-.md)命令，此方法非常有用。 不能将 **-zp**与标准的 Windows 页面文件一起使用，只能使用经过特别修改的页面文件。

<span id="_______-_______"></span>**-?**   
显示命令行帮助文本。

KD 将自动检测目标正在其上运行的平台。 不需要在 KD 命令行上指定目标。 旧语法（使用名称*I386KD*或*IA64KD*）已过时。

 

 





