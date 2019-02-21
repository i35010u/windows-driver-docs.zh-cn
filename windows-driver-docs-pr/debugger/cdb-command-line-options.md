---
title: CDB 命令行选项
description: CDB 或 NTSD 的第一次用户应使用调试使用 CDB 和 NTSD 部分开始。
ms.assetid: 34dbb695-19e4-4efc-83c7-3a94e5fcf269
keywords:
- CDB 命令行选项 Windows 调试
ms.date: 08/01/2018
topic_type:
- apiref
api_name:
- CDB Command-Line Options
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 37d49d78e2f4f04175faa580f44a0439bfe984fb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542153"
---
# <a name="cdb-command-line-options"></a>CDB 命令行选项


CDB 或 NTSD 的第一次用户应开头[调试使用 CDB 和 NTSD](debugging-using-cdb-and-ntsd.md)部分。

CDB 命令行使用以下语法：

```dbgcmd
cdb  [ -server ServerTransport | -remote ClientTransport ] 
[ -premote SmartClientTransport ] [-log{a|au|o|ou} LogFile]
[-2] [-d] [-ddefer] [-g] [-G] [-hd] [-lines] [-myob] [-bonc] 
[-n] [-o] [-s] [-v] [-w] [-cf "filename"] [-cfr "filename"] [-c "command"] 
[-robp] [-r BreakErrorLevel]  [-t PrintErrorLevel] 
[ -x{e|d|n|i} Exception ] [-x] [-clines lines] 
[-i ImagePath]  [-y SymbolPath] [-srcpath SourcePath] 
[-aExtension] [-failinc] [-noio] [-noinh] [-noshell] [-nosqm]
[-sdce] [-ses] [-sicv] [-sins] [-snc] [-snul] [-zp PageFile] 
[-sup] [-sflags 0xNumber] [-ee {masm|c++}]
[-e Event] [-pb] [-pd] [-pe] [-pr] [-pt Seconds] [-pv] 
[ -- | -p PID | -pn Name | -psn ServiceName | -z DumpFile | executable ] 
[-cimp] [-isd] [-kqm] [-pvr] [-version] [-vf] [-vf:<opts>] [-netsyms:{yes|no}]

cdb -iae 

cdb -iaec KeyString 

cdb -iu KeyString

cdb -QR Server 

cdb -wake pid 

cdb -?
```

NTSD 命令行语法等同于 CDB:

```dbgcmd
ntsd  [ -server ServerTransport | -remote ClientTransport ] 
[ -premote SmartClientTransport ] [-log{a|au|o|ou} LogFile]
[-2] [-d] [-ddefer] [-g] [-G] [-hd] [-lines] [-myob] [-bonc] 
[-n] [-o] [-s] [-v] [-w] [-cf "filename"] [-cfr "filename"] [-c "command"] 
[-robp] [-r BreakErrorLevel]  [-t PrintErrorLevel] 
[ -x{e|d|n|i} Exception ] [-x] [-clines lines] 
[-i ImagePath]  [-y SymbolPath] [-srcpath SourcePath] 
[-aExtension] [-failinc] [-noio] [-noinh] [-noshell] [-nosqm]
[-sdce] [-ses] [-sicv] [-sins] [-snc] [-snul] [-zp PageFile] 
[-sup] [-sflags 0xNumber] [-ee {masm|c++}] 
[-e Event] [-pb] [-pd] [-pe] [-pr] [-pt Seconds] [-pv] 
[ -- | -p PID | -pn Name | -psn ServiceName | -z DumpFile | executable ] 
[-cimp] [-isd] [-kqm] [-pvr] [-version] [-vf] [-vf:<opts>] [-netsyms:{yes|no}]

ntsd -iae 

ntsd -iaec KeyString 

ntsd -iu KeyString

ntsd -QR Server 

ntsd -wake PID 

ntsd -?
```

NTSD 和 CDB 之间唯一的区别是 NTSD 生成新的控制台窗口，而 CDB 继承调用它的窗口。 由于**启动**还可以使用命令来生成新的控制台窗口中，以下两个构造将提供相同的结果：

```dbgcmd
start cdb [parameters]
ntsd [parameters]
```

按照 CDB 和 NTSD 命令行选项的说明。 仅**的远程**， **-服务器**， **-g**并 **-G**选项是区分大小写。 可以使用正斜杠 （/） 替换初始的连字符。 可以连接不需要任何其他参数的选项-因此**cdb-o-d-G-g winmine**可以将其写作**cdb-odGg winmine**。

如果**的远程**或 **-server**选项，则它必须出现在之前在命令行上的任何其他选项。 如果*可执行文件*指定，则它必须显示命令行中的最后一个之后的任何文本*可执行文件*名称作为其自己的命令行参数传递给可执行程序。

## <a name="span-idddkcdbcommandlineoptionsdbgspanspan-idddkcdbcommandlineoptionsdbgspanparameters"></a><span id="ddk_cdb_command_line_options_dbg"></span><span id="DDK_CDB_COMMAND_LINE_OPTIONS_DBG"></span>参数


<span id="_______-server_______ServerTransport______"></span><span id="_______-server_______servertransport______"></span><span id="_______-SERVER_______SERVERTRANSPORT______"></span> **-server** *ServerTransport*   
创建可由其他调试器的调试服务器。 有关可能的说明*服务器传送*值，请参阅[**激活调试服务器**](activating-a-debugging-server.md)。 如果使用此参数，它必须是命令行中的第一个参数。

<span id="_______-remote_______ClientTransport______"></span><span id="_______-remote_______clienttransport______"></span><span id="_______-REMOTE_______CLIENTTRANSPORT______"></span> **-remote** *ClientTransport*   
创建调试客户端，并连接到已在运行的调试服务器。 有关可能的说明*ClientTransport*值，请参阅[**激活调试客户端**](activating-a-debugging-client.md)。 如果使用此参数，它必须是命令行中的第一个参数。

<span id="_______-premote_______SmartClientTransport______"></span><span id="_______-premote_______smartclienttransport______"></span><span id="_______-PREMOTE_______SMARTCLIENTTRANSPORT______"></span> **-premote** *SmartClientTransport*   
创建智能客户端，并连接到已在运行的进程服务器。 有关可能的说明*SmartClientTransport*值，请参阅[**激活智能客户端**](activating-a-smart-client.md)。

<span id="_______-2______"></span> **-2**   
如果目标应用程序*控制台应用程序*，此选项后，即可在新的控制台窗口。 （默认值是为目标的控制台应用程序与 CDB 或 NTSD 共享窗口。）

<span id="_______--______"></span> **--**   
调试客户端服务器运行时子系统 (CSRSS)。 有关详细信息，请参阅[调试 CSRSS](debugging-csrss.md)。

<span id="_______-a_______Extension______"></span><span id="_______-a_______extension______"></span><span id="_______-A_______EXTENSION______"></span> **-a** *扩展*   
设置默认扩展插件 DLL。 默认值是*userexts*。 必须有后的没有空格不能包含"a"、 和.dll 扩展名。 有关详细信息，并设置此默认设置的其他方法，请参阅[加载的调试器扩展 Dll](loading-debugger-extension-dlls.md)。

<span id="_______-bonc______"></span><span id="_______-BONC______"></span> **-bonc**   
如果指定此选项，则调试器将在会话开始时立即中断到目标。 连接到可能不当前分解为目标的调试服务器时，这是特别有用。

<span id="_______-c_________command______________"></span><span id="_______-C_________COMMAND______________"></span> **-c "** *command* **"**   
指定要在启动时运行的初始调试器命令。 此命令必须用引号括起来。 可以用分号分隔多个命令。 (如果有很长的命令列表，可能会更容易将其放在一个脚本，然后使用 **-c**选项与[  **$ &lt;，$&gt;&lt;，$&gt; &lt;，$$&gt; &lt; （运行脚本文件）** ](-----------------------a---run-script-file-.md)命令。)

如果要开始调试客户端，此命令必须适用于调试服务器中。 特定于客户端的命令，如 **.lsrcpath**不允许。

<span id="_______-cf_________filename______________"></span><span id="_______-CF_________FILENAME______________"></span> **-cf "** *filename* **"**   
指定的路径和脚本文件的名称。 启动调试器时，就立即执行此脚本文件。 如果*文件名*包含的空格，则必须用引号引起来。 如果省略路径，则假定当前目录。 如果 **-cf**不使用选项、 当前目录中的文件 ntsd.ini 用作脚本文件。 如果该文件不存在，会发生任何错误。 有关详细信息，请参阅[使用脚本文件](using-script-files.md)。

<span id="_______-cfr_________filename______________"></span><span id="_______-CFR_________FILENAME______________"></span> **-cfr "** *filename* **"**   
指定的路径和脚本文件的名称。 在启动调试器，并随时重新启动目标执行此脚本文件。 如果*文件名*包含的空格，则必须用引号引起来。 如果省略路径，则假定当前目录。 如果该文件不存在，会发生任何错误。 有关详细信息，请参阅[使用脚本文件](using-script-files.md)。

<span id="_______-cimp______"></span><span id="_______-CIMP______"></span> **-cimp**   
指示 CDB/NTSD 着手 DbgSrv 隐式命令行而不是一个显式的过程，才能运行。 此选项是 dbgsrv pc 的客户端。

<span id="_______-clines________lines______"></span><span id="_______-CLINES________LINES______"></span> **-clines** *lines*   
可以在远程调试过程中访问的命令历史记录中设置命令的大致的数目。 有关详细信息，以及更改此数字的其他方法，请参阅[使用调试器命令](using-debugger-commands.md)。

<span id="_______-d______"></span><span id="_______-D______"></span> **-d**   
传递的内核调试程序的此调试器的控制。 如果你正在调试 CSRSS，此控件重定向始终处于活动状态，即使 **-d**未指定。 (此选项不能为远程调试-期间使用使用 **-ddefer**相反。)请参阅[控制用户模式下调试程序与内核调试程序](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)有关详细信息。 此选项不能与任一结合使用 **-ddefer**选项或 **-noio**选项。

**请注意**  作为内核调试程序使用 WinDbg，如果许多 WinDbg 的常见功能将不可用在此方案中。 例如，无法使用局部变量窗口、 反汇编窗口中或调用堆栈窗口中，并且不能单步执行源代码。 这是因为 WinDbg 仅作为调试器 （NTSD 或 CDB） 的查看者在目标计算机上运行。

 

<span id="_______-ddefer______"></span><span id="_______-DDEFER______"></span> **-ddefer**   
将此调试器控制传递给内核调试器，除非调试客户端连接。 (这是变体 **-d** ，可以使用从调试服务器。)请参阅[控制用户模式下调试程序与内核调试程序](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)有关详细信息。 此选项不能与任一结合使用 **-d**选项或 **-noio**选项。

<span id="_______-e_______Event______"></span><span id="_______-e_______event______"></span><span id="_______-E_______EVENT______"></span> **-e** *Event*   
表示指定的事件发生调试器。 以编程方式启动调试器时，仅使用此选项。

<span id="_______-ee__masm_c___"></span><span id="_______-EE__MASM_C___"></span> **-ee** {**masm**|**c++**}  
设置默认表达式计算器。 如果**masm**指定，则将使用 MASM 表达式语法。 如果**c + +** 指定，则将使用 c + + 表达式语法。 如果 **-ee**省略选项，MASM 表达式语法将用作默认值。 请参阅[评估表达式](evaluating-expressions.md)有关详细信息。

<span id="_______-failinc______"></span><span id="_______-FAILINC______"></span> **-failinc**   
会导致调试器忽略任何可疑的符号。 在调试用户模式或内核模式的小型转储文件时，此选项将会阻止调试器加载任何模块不能映射其映像。 有关详细信息和控制这的其他方法，请参阅[SYMOPT\_EXACT\_符号](symbol-options.md#symopt-exact-symbols)。

<span id="_______-g______"></span><span id="_______-G______"></span> **-g**   
将忽略目标应用程序中的初始断点。 此选项将导致目标应用程序后仍继续运行已启动或 CDB 将附加到它，除非已设置另一个断点。 请参阅[初始断点](initial-breakpoint.md)有关详细信息。

<span id="_______-G______"></span><span id="_______-g______"></span> **-G**   
将忽略在进程终止时的最后一个断点。 默认情况下，CDB 映像 run-down 过程会停止。 此选项将导致 CDB 子终止时立即退出。 这具有与输入命令相同的效果**sxd epr**。 有关详细信息，请参阅[控制异常和事件](controlling-exceptions-and-events.md)。

<span id="_______-hd______"></span><span id="_______-HD______"></span> **-hd**   
 指定不应使用调试堆。 请参阅[调试用户模式进程使用 CDB](debugging-a-user-mode-process-using-cdb.md)有关详细信息。

<span id="_______-i_______ImagePath______"></span><span id="_______-i_______imagepath______"></span><span id="_______-I_______IMAGEPATH______"></span> **-i** *ImagePath*   
指定生成错误的可执行文件的位置。 如果路径包含空格，应括在引号中。

<span id="_______-iae______"></span><span id="_______-IAE______"></span> **-iae**   
将 CDB 作为事后调试器安装。 有关详细信息，请参阅[启用事后调试](enabling-postmortem-debugging.md)。

如果此操作成功，则不显示任何消息;如果失败，，显示一条错误消息。

**-Iae**参数必须不能与任何其他参数。 此命令将实际上不会启动 CDB。

<span id="_______-iaec_______KeyString______"></span><span id="_______-iaec_______keystring______"></span><span id="_______-IAEC_______KEYSTRING______"></span> **-iaec** *KeyString*   
将 CDB 作为事后调试器安装。 内容*KeyString*将追加到末尾**AeDebug**注册表项。 如果*KeyString*包含空格，则必须用引号引起来。 有关详细信息，请参阅[启用事后调试](enabling-postmortem-debugging.md)。

如果此操作成功，则不显示任何消息;如果失败，，显示一条错误消息。

**-Iaec**参数必须不能与任何其他参数。 此命令将实际上不会启动 CDB。

<span id="_______-isd______"></span><span id="_______-ISD______"></span> **-isd**   
打开创建\_忽略\_系统\_任何默认标记处理的作品。

<span id="_______-iu________KeyString______"></span><span id="_______-iu________keystring______"></span><span id="_______-IU________KEYSTRING______"></span> **-iu** *KeyString*   
将调试程序远程处理注册为 URL 类型，以便用户可以自动启动调试器远程客户端使用的 URL。 *KeyString*具有格式`remdbgeng://RemotingOption`。 *RemotingOption*是一个字符串，定义主题中定义的传输协议[**激活调试客户端**](activating-a-debugging-client.md)。 如果此操作成功，则不显示任何消息;如果失败，，显示一条错误消息。

**-Iu**参数必须不能与任何其他参数。 此命令将实际上不会启动 CDB。

<span id="_______-kqm______"></span><span id="_______-KQM______"></span> **-kqm**   
在静默模式下启动 CDB/NTSD。

<span id="_______-lines______"></span><span id="_______-LINES______"></span> **-lines**   
启用源行调试。 如果省略此选项，则[ **.lines （切换源行支持）** ](-lines--toggle-source-line-support-.md)命令将需要使用之前将允许源调试。 有关控制此的其他方法，请参阅[SYMOPT\_负载\_行](symbol-options.md#symopt-load-lines)。

<span id="_______-log_a_au_o_ou__LogFile"></span><span id="_______-log_a_au_o_ou__logfile"></span><span id="_______-LOG_A_AU_O_OU__LOGFILE"></span> **-log**{**a|au|o|ou**} *LogFile*  
开始将信息记入日志文件。 如果指定的文件已存在，则将覆盖如果 **-徽标**使用时，输出将追加到文件，如果使用-loga 或。 **-Logau**并 **-logou**选项作用类似于 **-loga**并 **-徽标**分别，除非日志文件是 Unicode 文件。 有关更多详细信息，请参阅[的日志文件保留 CDB](keeping-a-log-file-in-cdb.md)。

<span id="_______-myob______"></span><span id="_______-MYOB______"></span> **-myob**   
如果没有与 dbghelp.dll 版本不匹配，则调试器将继续运行。 (无需 **-myob**开关，这被认为是致命错误。)

<span id="_______-n______"></span><span id="_______-N______"></span> **-n**   
*干扰符号负载*:启用从符号处理程序的详细输出。 有关详细信息和控制这的其他方法，请参阅[SYMOPT\_调试](symbol-options.md#symopt-debug)。

<span id="_______-netsyms__yes_no_______"></span><span id="_______-NETSYMS__YES_NO_______"></span> **-netsyms {yes | 无}**   
允许或禁止从网络路径加载符号。

<span id="_______-noinh______"></span><span id="_______-NOINH______"></span> **-noinh**   
可以防止创建句柄继承从调试器调试程序的进程。 有关控制此的其他方法，请参阅[调试用户模式进程使用 CDB](debugging-a-user-mode-process-using-cdb.md)。

<span id="_______-noio______"></span><span id="_______-NOIO______"></span> **-noio**   
防止调试服务器正用于输入或输出。 输入将仅接受来自调试客户端 (以及任何初始命令或由指定的命令脚本 **-c**命令行选项)。

所有输出会都定向到调试客户端。 如果 NTSD 用于服务器，将根本创建没有控制台窗口。 有关更多详细信息，请参阅[**激活调试服务器**](activating-a-debugging-server.md)。 此选项不能与任一结合使用 **-d**选项或 **-ddefer**选项。

<span id="_______-noshell______"></span><span id="_______-NOSHELL______"></span> **-noshell**   
禁止所有 **.shell**命令。 此禁止将持续的时间运行调试器，即使开始新的调试会话。 有关详细信息，并了解的其他方式禁用 **.shell**命令，请参阅[使用 Shell 命令](using-shell-commands.md)。

<span id="_______-nosqm______"></span><span id="_______-NOSQM______"></span> **-nosqm**   
禁用遥测数据收集和上载。

<span id="_______-o______"></span><span id="_______-O______"></span> **-o**   
调试启动目标应用程序 （子进程） 的所有进程。 默认情况下，创建的一个正在调试的进程将运行它们通常要做。 有关控制此的其他方法，请参阅[调试用户模式进程使用 CDB](debugging-a-user-mode-process-using-cdb.md)。

<span id="_______-p_______PID______"></span><span id="_______-p_______pid______"></span><span id="_______-P_______PID______"></span> **-p** *PID*   
指定要调试的十进制进程 ID。 这用于调试已在运行的进程。 有关详细信息，请参阅[调试用户模式进程使用 CDB](debugging-a-user-mode-process-using-cdb.md)。

<span id="_______-pb______"></span><span id="_______-PB______"></span> **-pb**   
防止调试器附加到目标进程时请求初始被侵入的情形。 如果应用程序已挂起，或者如果你想要避免在目标中创建被侵入的情形线程，这可以很有用。

<span id="_______-pd______"></span><span id="_______-PD______"></span> **-pd**   
导致目标应用程序不会终止调试会话结束时。 请参阅[结束调试会话中 CDB](ending-a-debugging-session-in-cdb.md)有关详细信息。

<span id="_______-pe______"></span><span id="_______-PE______"></span> **-pe**   
指示已在调试目标应用程序。 请参阅[重新连接到目标应用程序](reattaching-to-the-target-application.md)有关详细信息。

<span id="_______-pn_______Name______"></span><span id="_______-pn_______name______"></span><span id="_______-PN_______NAME______"></span> **-pn** *Name*   
指定要调试的进程的名称。 （此名称必须是唯一的。）这用于调试已在运行的进程。

<span id="_______-pr______"></span><span id="_______-PR______"></span> **-pr**   
导致调试器开始运行时它将附加到它的目标进程。 如果应用程序已挂起状态，并且您不希望继续执行，这很有用。

<span id="_______-psn_______ServiceName______"></span><span id="_______-psn_______servicename______"></span><span id="_______-PSN_______SERVICENAME______"></span> **-psn** *ServiceName*   
指定要调试的过程中包含的服务的名称。 这用于调试已在运行的进程。

<span id="_______-pt_______Seconds______"></span><span id="_______-pt_______seconds______"></span><span id="_______-PT_______SECONDS______"></span> **-pt** *Seconds*   
以秒为单位指定中断超时。 默认值为 30。 请参阅[控制目标](controlling-the-target.md)有关详细信息。

<span id="_______-pv______"></span><span id="_______-PV______"></span> **-pv**   
指定调试器应 noninvasively 附加到目标进程。 有关详细信息，请参阅[非侵入调试 （用户模式）](noninvasive-debugging--user-mode-.md)。

<span id="_______-pvr______"></span><span id="_______-PVR______"></span> **-pvr**   
工作方式类似于 **-pv**不同之处在于目标进程不会挂起。

<span id="_______-QR_______Server______"></span><span id="_______-qr_______server______"></span><span id="_______-QR_______SERVER______"></span> **-QR** *Server*   
列出在指定的网络服务器上运行的所有调试服务器。 双反斜杠 (\\ \)前面*Server*是可选的。 请参阅[**搜索调试服务器**](searching-for-debugging-servers.md)有关详细信息。

**-QR**参数不能用于任何其他参数。 此命令将实际上不会启动 CDB。

<span id="_______-r________BreakErrorLevel______"></span><span id="_______-r________breakerrorlevel______"></span><span id="_______-R________BREAKERRORLEVEL______"></span> **-r** *BreakErrorLevel*   
指定将导致目标来中断调试器将错误级别。 这是一个十进制数等于 0、 1、 2 或 3。 可能的值如下：

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">值</th>
<th align="left">Constant</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>NONE</p></td>
<td align="left"><p>不会中断上的任何错误。</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>错误</p></td>
<td align="left"><p>在错误级别的调试事件上中断。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>2</p></td>
<td align="left"><p>MINORERROR</p></td>
<td align="left"><p>中断上 MINORERROR 和错误级别的调试事件。</p></td>
</tr>
<tr class="even">
<td align="left"><p>3</p></td>
<td align="left"><p>警告</p></td>
<td align="left"><p>在警告、 MINORERROR 和错误级别的调试事件上中断。</p></td>
</tr>
</tbody>
</table>

 

此错误级别仅在已检查版本的 Microsoft Windows 中具有含义。 默认值为 1。

<span id="_______-robp______"></span><span id="_______-ROBP______"></span> **-robp**   
这允许 CDB 只读内存页上设置断点。 （默认值是此类操作失败。）

<span id="_______-s______"></span><span id="_______-S______"></span> **-s**   
禁用延迟符号加载。 这将减慢进程启动。 有关详细信息和控制这的其他方法，请参阅[SYMOPT\_延期\_加载](symbol-options.md#symopt-deferred-loads)。

<span id="_______-sdce______"></span><span id="_______-SDCE______"></span> **-sdce**   
使调试器显示**文件访问错误**符号加载过程中的对话框。 有关详细信息和控制这的其他方法，请参阅[SYMOPT\_失败\_严重\_错误](symbol-options.md#symopt-fail-critical-errors)。

<span id="_______-ses______"></span><span id="_______-SES______"></span> **-ses**   
使调试器执行的所有符号文件严格评估，并忽略任何可疑的符号。 有关详细信息和控制这的其他方法，请参阅[SYMOPT\_EXACT\_符号](symbol-options.md#symopt-exact-symbols)。

<span id="_______-sflags_0x_______Number______"></span><span id="_______-sflags_0x_______number______"></span><span id="_______-SFLAGS_0X_______NUMBER______"></span> **-sflags 0 x** *数*   
一次性设置所有的符号处理程序选项。 *数*应能带有前缀的十六进制数**0x** -而无需十进制**0x**允许，则允许而符号选项是二进制的标志，因此建议十六进制。 应谨慎，使用此选项，因为它将替代所有符号处理程序默认值。 有关详细信息，请参阅[设置符号选项](symbol-options.md)。

<span id="_______-sicv______"></span><span id="_______-SICV______"></span> **-sicv**   
导致要忽略 CV 记录的符号处理程序。 有关详细信息和控制这的其他方法，请参阅[SYMOPT\_忽略\_CVREC](symbol-options.md#symopt-ignore-cvrec)。

<span id="_______-sins______"></span><span id="_______-SINS______"></span> **-sins**   
会导致调试器忽略符号路径和可执行文件映像路径环境变量。 有关详细信息，请参阅[SYMOPT\_忽略\_NT\_SYMPATH](symbol-options.md#symopt-ignore-nt-sympath)。

<span id="_______-snc______"></span><span id="_______-SNC______"></span> **-snc**   
使调试器后，若要关闭 c + + 转换。 有关详细信息和控制这的其他方法，请参阅[SYMOPT\_否\_CPP](symbol-options.md#symopt-no-cpp)。

<span id="_______-snul______"></span><span id="_______-SNUL______"></span> **-snul**   
禁用自动符号加载的非限定名称。 有关详细信息和控制这的其他方法，请参阅[SYMOPT\_否\_UNQUALIFIED\_加载](symbol-options.md#symopt-no-unqualified-loads)。

<span id="_______-srcpath_______SourcePath______"></span><span id="_______-srcpath_______sourcepath______"></span><span id="_______-SRCPATH_______SOURCEPATH______"></span> **-srcpath** *SourcePath*   
指定源文件搜索路径。 用分号 （;） 分隔多个路径。 如果路径包含空格，应括在引号中。 有关详细信息，以及更改此路径的其他方法，请参阅[源路径](source-path.md)。

<span id="_______-sup______"></span><span id="_______-SUP______"></span> **-sup**   
导致要在每个符号搜索期间搜索公共符号表的符号处理程序。 有关详细信息和控制这的其他方法，请参阅[SYMOPT\_自动\_PUBLICS](symbol-options.md#symopt-auto-publics)。

<span id="_______-t________PrintErrorLevel______"></span><span id="_______-t________printerrorlevel______"></span><span id="_______-T________PRINTERRORLEVEL______"></span> **-t** *PrintErrorLevel*   
指定将导致调试程序来显示一条错误消息的错误级别。 这是一个十进制数等于 0、 1、 2 或 3。 可能的值如下：

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">值</th>
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
启用从调试器的详细输出。

<span id="_______-version______"></span><span id="_______-VERSION______"></span> **-version**   
打印的调试器版本字符串。

<span id="_______-vf______"></span><span id="_______-VF______"></span> **-vf**   
启用默认 ApplicationVerifier 设置。

<span id="_______-vf________opts_"></span><span id="_______-VF________OPTS_"></span> **-vf:** *&lt;opts&gt;*  
启用给定的 ApplicationVerifier 设置。

<span id="_______-w______"></span><span id="_______-W______"></span> **-w**   
指定要调试在一个单独的 VDM 的 16 位应用程序。

<span id="_______-wake_______PID______"></span><span id="_______-wake_______pid______"></span><span id="_______-WAKE_______PID______"></span> **-wake** *PID*   
原因睡眠模式下，若要通过指定其进程 ID 的用户模式下调试程序结束*PID*。 在睡眠模式期间，必须在目标计算机上发出此命令。 请参阅[控制用户模式下调试程序与内核调试程序](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)有关详细信息。

**-唤醒**参数不能用于任何其他参数。 此命令将实际上不会启动 CDB。

<span id="_______-x_e_d_n_i__Exception"></span><span id="_______-x_e_d_n_i__exception"></span><span id="_______-X_E_D_N_I__EXCEPTION"></span> **-x**{**e**|**d**|**n**|**i**} *Exception*  
指定的事件发生时，可控制调试器的行为。 *异常*可以是异常数或事件代码。 您可以指定此选项多次，以控制不同的事件。 请参阅[控制异常和事件](controlling-exceptions-and-events.md)为详细信息和控制这些设置的其他方法。

<span id="_______-x______"></span><span id="_______-X______"></span> **-x**   
禁用首次访问冲突异常时中断。 访问冲突的第二个匹配项将进入调试器。 这是与相同 **-xd av**。

<span id="_______-y_______SymbolPath______"></span><span id="_______-y_______symbolpath______"></span><span id="_______-Y_______SYMBOLPATH______"></span> **-y** *SymbolPath*   
指定符号搜索路径。 用分号 （;） 分隔多个路径。 如果路径包含空格，应括在引号中。 有关详细信息，以及更改此路径的其他方法，请参阅[符号路径](symbol-path.md)。

<span id="_______-z_______DumpFile______"></span><span id="_______-z_______dumpfile______"></span><span id="_______-Z_______DUMPFILE______"></span> **-z** *DumpFile*   
指定要调试的崩溃转储文件的名称。 如果路径和文件名称包含空格，这必须用引号括起来。 可以通过包含多个同时打开多个转储文件**z**选项，每个后跟一个不同*DumpFile*值。 有关详细信息，请参阅[分析用户模式转储文件](analyzing-a-user-mode-dump-file.md)。

<span id="_______-zp_______PageFile______"></span><span id="_______-zp_______pagefile______"></span><span id="_______-ZP_______PAGEFILE______"></span> **-zp** *PageFile*   
指定修改的页面文件的名称。 如果您正在调试转储文件，并且想要使用，这很有用[ **.pagein （内存中的页）** ](-pagein--page-in-memory-.md)命令。 不能使用 **-zp**与标准的 Windows 页文件--可以使用仅专门修改页面文件。

<span id="_______executable______"></span><span id="_______EXECUTABLE______"></span> *executable*   
指定可执行进程的命令行。 这用于启动新进程，并对其进行调试。 这必须是命令行上的最后一个项目。 可执行文件的名称传递给可执行文件作为其参数字符串后的所有文本。

<span id="_______-_______"></span> **-?**   
显示命令行帮助文本。

启动调试器时**启动 |运行**或从命令提示符窗口中，指定用于目标应用程序后应用程序的文件名称的参数。 例如：

```dbgcmd
cdb myexe arg1arg2
```

 

 





