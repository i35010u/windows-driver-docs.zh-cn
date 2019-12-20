---
title: CDB 命令行选项
description: CDB 或 NTSD 的首次用户应从使用 CDB 和 NTSD 部分进行调试开始。
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
ms.openlocfilehash: 5bd69b938be93ed1a876915e945495cd6dc34a92
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75209399"
---
# <a name="cdb-command-line-options"></a>CDB 命令行选项


CDB 或 NTSD 的首次用户应从[使用 CDB 和 ntsd](debugging-using-cdb-and-ntsd.md)部分进行调试开始。

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

NTSD 命令行语法与 CDB 的命令行语法相同：

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

NTSD 和 CDB 之间唯一的区别是，NTSD 会生成新的控制台窗口，而 CDB 会继承从中调用它的窗口。 由于 "**启动**" 命令还可用于生成新的控制台窗口，因此以下两个构造将产生相同的结果：

```dbgcmd
start cdb [parameters]
ntsd [parameters]
```

下面是 CDB 和 NTSD 命令行选项的说明。 只有 **-remote**、 **-server**、 **-g**和 **-g**选项区分大小写。 可以使用正斜杠（/）替换初始连字符。 可以连接不采用任何其他参数的选项，因此，可以将**cdb-o-g** -g winmine 编写为**cdb-odGg winmine**。

如果使用了 **-remote**或 **-server**选项，则它必须出现在命令行上的任何其他选项之前。 如果指定了*可执行文件*，则它必须出现在命令行的最后;*可执行文件*名称后的任何文本都作为其自身的命令行参数传递给可执行程序。

## <a name="span-idddk_cdb_command_line_options_dbgspanspan-idddk_cdb_command_line_options_dbgspanparameters"></a><span id="ddk_cdb_command_line_options_dbg"></span><span id="DDK_CDB_COMMAND_LINE_OPTIONS_DBG"></span>Parameters


<span id="_______-server_______ServerTransport______"></span><span id="_______-server_______servertransport______"></span><span id="_______-SERVER_______SERVERTRANSPORT______"></span>**-server** *ServerTransport*   
创建可由其他调试器访问的调试服务器。 有关可能的*ServerTransport*值的说明，请参阅[**激活调试服务器**](activating-a-debugging-server.md)。 使用此参数时，该参数必须是命令行中的第一个参数。

<span id="_______-remote_______ClientTransport______"></span><span id="_______-remote_______clienttransport______"></span><span id="_______-REMOTE_______CLIENTTRANSPORT______"></span>**-remote** *ClientTransport*   
创建调试客户端，并连接到已在运行的调试服务器。 有关可能的*ClientTransport*值的说明，请参阅[**激活调试客户端**](activating-a-debugging-client.md)。 使用此参数时，该参数必须是命令行中的第一个参数。

<span id="_______-premote_______SmartClientTransport______"></span><span id="_______-premote_______smartclienttransport______"></span><span id="_______-PREMOTE_______SMARTCLIENTTRANSPORT______"></span>**-premote** *SmartClientTransport*   
创建智能客户端，并连接到已在运行的进程服务器。 有关可能的*SmartClientTransport*值的说明，请参阅[**激活智能客户端**](activating-a-smart-client.md)。

<span id="_______-2______"></span>**-2**   
如果目标应用程序是一个*控制台应用程序*，则此选项会使其在新的控制台窗口中出现。 （对于目标控制台应用程序，使用 CDB 或 NTSD 共享窗口的默认值为。）

<span id="_______--______"></span>**--**   
调试客户端服务器运行时子系统（CSRSS）。 有关详细信息，请参阅[调试 CSRSS](debugging-csrss.md)。

<span id="_______-a_______Extension______"></span><span id="_______-a_______extension______"></span><span id="_______-A_______EXTENSION______"></span>**-** *扩展*   
设置默认扩展 DLL。 默认值为*userexts*。 "A" 后面一定不能有空格，并且不得包含 .dll 扩展名。 有关详细信息和设置此默认设置的其他方法，请参阅[加载调试器扩展 dll](loading-debugger-extension-dlls.md)。

<span id="_______-bonc______"></span><span id="_______-BONC______"></span>**-bonc**   
如果指定此选项，则调试器将在会话开始时立即进入目标。 这在连接到可能当前未分解到目标的调试服务器时特别有用。

<span id="_______-c_________command______________"></span><span id="_______-C_________COMMAND______________"></span>**-c "** *command* **"**   
指定要在启动时运行的初始调试器命令。 此命令必须用引号引起来。 可以用分号分隔多个命令。 （如果您有一个长命令列表，则可以更容易地将其放入脚本，然后将 **-c**选项与[**$&lt;，$&gt;&lt;，$&gt;&lt;，$ $&gt;&lt; （运行脚本文件）**](-----------------------a---run-script-file-.md)命令一起使用。）

如果要启动调试客户端，则必须将此命令用于调试服务器。 不允许使用客户端特定的命令（如**lsrcpath** ）。

<span id="_______-cf_________filename______________"></span><span id="_______-CF_________FILENAME______________"></span>**-cf "** *filename* **"**   
指定脚本文件的路径和名称。 启动调试器后，将立即执行该脚本文件。 如果*filename*包含空格，则必须用引号将其引起来。 如果省略该路径，则假定为当前目录。 如果未使用 **-cf**选项，则使用当前目录中的文件 ntsd 作为脚本文件。 如果文件不存在，则不会发生错误。 有关详细信息，请参阅[使用脚本文件](using-script-files.md)。

<span id="_______-cfr_________filename______________"></span><span id="_______-CFR_________FILENAME______________"></span>**-cfr "** *filename* **"**   
指定脚本文件的路径和名称。 一旦启动调试器，就会执行该脚本文件，并在每次重新启动目标时执行。 如果*filename*包含空格，则必须用引号将其引起来。 如果省略该路径，则假定为当前目录。 如果文件不存在，则不会发生错误。 有关详细信息，请参阅[使用脚本文件](using-script-files.md)。

<span id="_______-cimp______"></span><span id="_______-CIMP______"></span>**-cimp**   
指示 CDB/NTSD 以 DbgSrv 的隐式命令行（而不是要运行的显式进程）开头。 此选项是 dbgsrv 的客户端。

<span id="_______-clines________lines______"></span><span id="_______-CLINES________LINES______"></span>**-clines** *行*   
设置在远程调试过程中可以访问的命令历史记录中的大概命令数。 有关详细信息以及其他更改此数字的方法，请参阅[使用调试器命令](using-debugger-commands.md)。

<span id="_______-d______"></span><span id="_______-D______"></span>**-d**   
将此调试器的控制权传递给内核调试器。 如果正在调试 CSRSS，此控件重定向始终处于活动状态，即使未指定 **-d**也是如此。 （在远程调试过程中不能使用此选项--请改用**ddefer** 。）有关详细信息，请参阅[从内核调试器控制用户模式调试器](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)。 此选项不能与 **-ddefer**选项或 **-noio**选项一起使用。

**请注意**  如果使用 windbg 作为内核调试器，则在此方案中，很多熟悉的 windbg 功能不可用。 例如，不能使用 "局部变量" 窗口、"反汇编" 窗口或 "调用堆栈" 窗口，也不能单步执行源代码。 这是因为 WinDbg 只充当在目标计算机上运行的调试器（NTSD 或 CDB）的查看器。

 

<span id="_______-ddefer______"></span><span id="_______-DDEFER______"></span>**-ddefer**   
将此调试器的控制权传递给内核调试器，除非连接了调试客户端。 （这是一个 **-d**变体，可以从调试服务器使用。）有关详细信息，请参阅[从内核调试器控制用户模式调试器](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)。 此选项不能与 **-d**选项或 **-noio**选项一起使用。

<span id="_______-e_______Event______"></span><span id="_______-e_______event______"></span><span id="_______-E_______EVENT______"></span>**-e** *事件*   
向调试器发出指定事件的信号。 仅当以编程方式启动调试器时才使用此选项。

<span id="_______-ee__masm_c___"></span><span id="_______-EE__MASM_C___"></span>**-ee** {**masm**|**c + +**}  
设置默认表达式计算器。 如果指定了**masm** ，将使用 masm 表达式语法。 如果指定**c + +** ， C++则使用 expression 语法。 如果省略 **-ee**选项，则将使用 MASM 表达式语法作为默认值。 有关详细信息，请参阅[计算表达式](evaluating-expressions.md)。

<span id="_______-failinc______"></span><span id="_______-FAILINC______"></span>**-failinc**   
导致调试器忽略任何有问题的符号。 调试用户模式或内核模式小型转储文件时，此选项还会阻止调试器加载其图像无法映射的任何模块。 有关详细信息和控制此方法的其他方法，请参阅[SYMOPT\_精确\_符号](symbol-options.md#symopt-exact-symbols)。

<span id="_______-g______"></span><span id="_______-G______"></span>**-g**   
忽略目标应用程序中的初始断点。 此选项将导致目标应用程序在启动后继续运行，或将 CDB 附加到该应用程序，除非已设置了另一个断点。 有关详细信息，请参阅[初始断点](initial-breakpoint.md)。

<span id="_______-G______"></span><span id="_______-g______"></span>**-G**   
在进程终止时忽略最终断点。 默认情况下，在映像运行进程中，CDB 停止。 当子级终止时，此选项将导致 CDB 立即退出。 这与输入命令**sxd epr**相同。 有关详细信息，请参阅[控制异常和事件](controlling-exceptions-and-events.md)。

<span id="_______-hd______"></span><span id="_______-HD______"></span>**-hd**   
 指定不应使用调试堆。 有关详细信息，请参阅[使用 CDB 调试用户模式进程](debugging-a-user-mode-process-using-cdb.md)。

<span id="_______-i_______ImagePath______"></span><span id="_______-i_______imagepath______"></span><span id="_______-I_______IMAGEPATH______"></span>**-i** *ImagePath*   
指定生成错误的可执行文件的位置。 如果路径包含空格，则应该用引号将其引起来。

<span id="_______-iae______"></span><span id="_______-IAE______"></span>**-iae**   
将 CDB 安装为事后调试器。 有关详细信息，请参阅[启用事后调试](enabling-postmortem-debugging.md)。

如果此操作成功，则不会显示任何消息;如果失败，将显示一条错误消息。

**-Iae**参数不得与任何其他参数一起使用。 此命令实际上不会启动 CDB。

<span id="_______-iaec_______KeyString______"></span><span id="_______-iaec_______keystring______"></span><span id="_______-IAEC_______KEYSTRING______"></span>**-iaec** *KeyString*   
将 CDB 安装为事后调试器。 *KeyString*的内容将追加到**AeDebug**注册表项的结尾。 如果*KeyString*包含空格，则必须用引号将其引起来。 有关详细信息，请参阅[启用事后调试](enabling-postmortem-debugging.md)。

如果此操作成功，则不会显示任何消息;如果失败，将显示一条错误消息。

**-Iaec**参数不得与任何其他参数一起使用。 此命令实际上不会启动 CDB。

<span id="_______-isd______"></span><span id="_______-ISD______"></span>**-isd**   
为任何进程创建启用 "创建\_忽略\_系统\_默认标志。

<span id="_______-iu________KeyString______"></span><span id="_______-iu________keystring______"></span><span id="_______-IU________KEYSTRING______"></span>**-iu** *KeyString*   
将调试器远程处理注册为 URL 类型，以便用户可以使用 URL 自动启动调试器远程客户端。 *KeyString*的格式 `remdbgeng://RemotingOption`。 *RemotingOption*是一个字符串，它定义在[**激活调试客户端**](activating-a-debugging-client.md)主题中定义的传输协议。 如果此操作成功，则不会显示任何消息;如果失败，将显示一条错误消息。

**-Iu**参数不得与任何其他参数一起使用。 此命令实际上不会启动 CDB。

<span id="_______-kqm______"></span><span id="_______-KQM______"></span>**-kqm**   
在安静模式下启动 CDB/NTSD。

<span id="_______-lines______"></span><span id="_______-LINES______"></span>**-行**   
启用源代码行调试。 如果省略此选项，则在允许进行源调试之前，必须使用 "[**行（切换源代码行支持）**](-lines--toggle-source-line-support-.md) " 命令。 有关控制此情况的其他方法，请参阅[SYMOPT\_LOAD\_行](symbol-options.md#symopt-load-lines)。

<span id="_______-log_a_au_o_ou__LogFile"></span><span id="_______-log_a_au_o_ou__logfile"></span><span id="_______-LOG_A_AU_O_OU__LOGFILE"></span>**-log**{**a | au | o | ou**}*日志文件*  
开始将信息记录到日志文件。 如果指定的文件已存在，则会在使用 **-徽标**时覆盖该文件，如果使用-loga，则输出将追加到该文件。 **-Logau**和 **-logou**选项分别与 **-loga**和 **-徽标**分别操作，只不过日志文件是 Unicode 文件。 有关更多详细信息，请参阅[在 CDB 中保留日志文件](keeping-a-log-file-in-cdb.md)。

<span id="_______-myob______"></span><span id="_______-MYOB______"></span>**-myob**   
如果版本与 dbghelp.dll 不匹配，则调试器将继续运行。 （如果没有 **-myob**开关，此错误将被视为错误。）

<span id="_______-n______"></span><span id="_______-N______"></span>**-n**   
*干扰符号加载*：从符号处理程序启用详细输出。 有关详细信息和控制此方法的其他方法，请参阅[SYMOPT\_调试](symbol-options.md#symopt-debug)。

<span id="_______-netsyms__yes_no_______"></span><span id="_______-NETSYMS__YES_NO_______"></span>**-netsyms {yes | no}**   
允许或禁止从网络路径加载符号。

<span id="_______-noinh______"></span><span id="_______-NOINH______"></span>**-noinh**   
阻止调试器创建的进程从调试器继承句柄。 有关控制此操作的其他方法，请参阅[使用 CDB 调试用户模式进程](debugging-a-user-mode-process-using-cdb.md)。

<span id="_______-noio______"></span><span id="_______-NOIO______"></span>**-noio**   
阻止调试服务器用于输入或输出。 仅从调试客户端（以及由 **-c**命令行选项指定的任何初始命令或命令脚本）接受输入。

所有输出都将定向到调试客户端。 如果服务器使用了 NTSD，则根本不会创建控制台窗口。 有关更多详细信息，请参阅[**激活调试服务器**](activating-a-debugging-server.md)。 此选项不能与 **-d**选项或 **-ddefer**选项一起使用。

<span id="_______-noshell______"></span><span id="_______-NOSHELL______"></span>**-noshell**   
禁止全部**shell**命令。 即使启动了新的调试会话，此禁止仍将在调试器运行的时间结束。 有关详细信息，以及其他禁用**shell**命令的方法，请参阅[使用 shell 命令](using-shell-commands.md)。

<span id="_______-nosqm______"></span><span id="_______-NOSQM______"></span>**-nosqm**   
禁用遥测数据收集和上载。

<span id="_______-o______"></span><span id="_______-O______"></span>**-o**   
调试由目标应用程序启动的所有进程（子进程）。 默认情况下，由正在调试的进程创建的进程将按正常运行的方式运行。 有关控制此操作的其他方法，请参阅[使用 CDB 调试用户模式进程](debugging-a-user-mode-process-using-cdb.md)。

<span id="_______-p_______PID______"></span><span id="_______-p_______pid______"></span><span id="_______-P_______PID______"></span>**-p** *PID*   
指定要调试的十进制进程 ID。 这用于调试已经在运行的进程。 有关详细信息，请参阅[使用 CDB 调试用户模式进程](debugging-a-user-mode-process-using-cdb.md)。

<span id="_______-pb______"></span><span id="_______-PB______"></span>**-pb**   
阻止调试器在附加到目标进程时请求初始中断。 如果应用程序已挂起，或者您想要避免在目标中创建一个中断线程，这会很有用。

<span id="_______-pd______"></span><span id="_______-PD______"></span>**-pd**   
使目标应用程序不会在调试会话结束时终止。 有关详细信息，请参阅[在 CDB 中结束调试会话](ending-a-debugging-session-in-cdb.md)。

<span id="_______-pe______"></span><span id="_______-PE______"></span>**-pe**   
指示目标应用程序已在进行调试。 有关详细信息，请参阅[重新附加到目标应用程序](reattaching-to-the-target-application.md)。

<span id="_______-pn_______Name______"></span><span id="_______-pn_______name______"></span><span id="_______-PN_______NAME______"></span>**-pn** *Name*   
指定要调试的进程的名称。 （此名称必须是唯一的。）这用于调试已经在运行的进程。

<span id="_______-pr______"></span><span id="_______-PR______"></span>**-pr**   
导致调试器在附加到目标进程时启动该进程。 这在应用程序已挂起且你希望它恢复执行时非常有用。

<span id="_______-psn_______ServiceName______"></span><span id="_______-psn_______servicename______"></span><span id="_______-PSN_______SERVICENAME______"></span>**-psn** *ServiceName*   
指定要调试的进程中包含的服务的名称。 这用于调试已经在运行的进程。

<span id="_______-pt_______Seconds______"></span><span id="_______-pt_______seconds______"></span><span id="_______-PT_______SECONDS______"></span>**-pt** *秒*   
指定中断超时（以秒为单位）。 默认值为30。 有关详细信息，请参阅[控制目标](controlling-the-target.md)。

<span id="_______-pv______"></span><span id="_______-PV______"></span>**-pv**   
指定调试器应附加到目标进程 noninvasively。 有关详细信息，请参阅[Noninvasive 调试（用户模式）](noninvasive-debugging--user-mode-.md)。

<span id="_______-pvr______"></span><span id="_______-PVR______"></span>**-pvr**   
类似于 **-pv** ，但目标进程不会挂起。

<span id="_______-QR_______Server______"></span><span id="_______-qr_______server______"></span><span id="_______-QR_______SERVER______"></span>**-QR** *服务器*   
列出在指定的网络服务器上运行的所有调试服务器。 双反斜杠（\\\) 上一*服务器*是可选的。 有关详细信息，请参阅[**搜索调试服务器**](searching-for-debugging-servers.md)。

**-QR**参数不能与任何其他参数一起使用。 此命令实际上不会启动 CDB。

<span id="_______-r________BreakErrorLevel______"></span><span id="_______-r________breakerrorlevel______"></span><span id="_______-R________BREAKERRORLEVEL______"></span>**-r** *BreakErrorLevel*   
指定将导致目标中断到调试器中的错误级别。 这是一个十进制数，等于0、1、2或3。 可能的值如下：

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
<td align="left"><p>不要在出现任何错误时中断。</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>错误</p></td>
<td align="left"><p>错误级别调试事件时中断。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>2</p></td>
<td align="left"><p>MINORERROR</p></td>
<td align="left"><p>在 MINORERROR 和错误级别调试事件时中断。</p></td>
</tr>
<tr class="even">
<td align="left"><p>3</p></td>
<td align="left"><p>警告</p></td>
<td align="left"><p>在警告、MINORERROR 和错误级别调试事件时中断。</p></td>
</tr>
</tbody>
</table>

 

此错误级别仅在已检查的 Microsoft Windows 版本中具有意义。 默认值为 1。 在 Windows 10 版本1803之前，已检查的生成在较早版本的 Windows 上可用。

<span id="_______-robp______"></span><span id="_______-ROBP______"></span>**-robp**   
这允许 CDB 在只读内存页面上设置断点。 （此类操作的默认值为失败。）

<span id="_______-s______"></span><span id="_______-S______"></span>**-s**   
禁用延迟符号加载。 这会降低进程启动的速度。 有关详细信息和控制此方法的其他方法，请参阅[SYMOPT\_延迟\_负载](symbol-options.md#symopt-deferred-loads)。

<span id="_______-sdce______"></span><span id="_______-SDCE______"></span>**-sdce**   
使调试器在符号加载过程中显示**文件访问错误**对话框。 有关详细信息，请参阅[SYMOPT\_失败\_严重\_错误](symbol-options.md#symopt-fail-critical-errors)。

<span id="_______-ses______"></span><span id="_______-SES______"></span>**-ses**   
使调试器对所有符号文件执行严格的评估，并忽略任何有问题的符号。 有关详细信息和控制此方法的其他方法，请参阅[SYMOPT\_精确\_符号](symbol-options.md#symopt-exact-symbols)。

<span id="_______-sflags_0x_______Number______"></span><span id="_______-sflags_0x_______number______"></span><span id="_______-SFLAGS_0X_______NUMBER______"></span>**-sflags 0x** *Number*   
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
指定源文件搜索路径。 使用分号（;) 分隔多个路径。 如果路径包含空格，则应该用引号将其引起来。 有关详细信息，请参阅[源路径](source-path.md)。

<span id="_______-sup______"></span><span id="_______-SUP______"></span>**-sup**   
使符号处理程序在每个符号搜索过程中搜索公共符号表。 有关详细信息和控制此方法的其他方法，请参阅[SYMOPT\_AUTO\_PUBLICS](symbol-options.md#symopt-auto-publics)。

<span id="_______-t________PrintErrorLevel______"></span><span id="_______-t________printerrorlevel______"></span><span id="_______-T________PRINTERRORLEVEL______"></span>**-t** *PrintErrorLevel*   
指定将导致调试器显示错误消息的错误级别。 这是一个十进制数，等于0、1、2或3。 可能的值如下：

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

 

此错误级别仅在已检查的 Microsoft Windows 版本中具有意义。 在 Windows 10 版本1803之前，已检查的生成在 windows 的早期版本上可用。 默认值为 1。

<span id="_______-v______"></span><span id="_______-V______"></span>**-v**   
从调试器启用详细输出。

<span id="_______-version______"></span><span id="_______-VERSION______"></span>**-版本**   
打印调试器版本字符串。

<span id="_______-vf______"></span><span id="_______-VF______"></span>**-vf**   
启用默认 ApplicationVerifier 设置。

<span id="_______-vf________opts_"></span><span id="_______-VF________OPTS_"></span>**-vf：** *&lt;的&gt;*  
启用给定的 ApplicationVerifier 设置。

<span id="_______-w______"></span><span id="_______-W______"></span>**-w**   
指定在单独的 VDM 中调试16位应用程序。

<span id="_______-wake_______PID______"></span><span id="_______-wake_______pid______"></span><span id="_______-WAKE_______PID______"></span>**-唤醒** *PID*   
使睡眠模式对于其进程 ID 由*PID*指定的用户模式调试器结束。 在睡眠模式下，必须在目标计算机上发出此命令。 有关详细信息，请参阅[从内核调试器控制用户模式调试器](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)。

**-唤醒**参数不应与任何其他参数一起使用。 此命令实际上不会启动 CDB。

<span id="_______-x_e_d_n_i__Exception"></span><span id="_______-x_e_d_n_i__exception"></span><span id="_______-X_E_D_N_I__EXCEPTION"></span>**-x**{**e**|**d**|**n**|**i**}*异常*  
控制调试器在发生指定事件时的行为。 *异常*可以是异常号或事件代码。 可以多次指定此选项以控制不同的事件。 有关详细信息和其他控制这些设置的方法，请参阅[控制异常和事件](controlling-exceptions-and-events.md)。

<span id="_______-x______"></span><span id="_______-X______"></span>**-x**   
禁用对访问冲突异常的第一次中断。 第二次出现访问冲突时将中断调试器。 这与 **-xd av**相同。

<span id="_______-y_______SymbolPath______"></span><span id="_______-y_______symbolpath______"></span><span id="_______-Y_______SYMBOLPATH______"></span>**-y** *SymbolPath*   
指定符号搜索路径。 使用分号（;) 分隔多个路径。 如果路径包含空格，则应该用引号将其引起来。 有关详细信息和更改此路径的其他方式，请参阅[符号路径](symbol-path.md)。

<span id="_______-z_______DumpFile______"></span><span id="_______-z_______dumpfile______"></span><span id="_______-Z_______DUMPFILE______"></span>**-z** *DumpFile*   
指定要调试的故障转储文件的名称。 如果路径和文件名包含空格，则必须用引号将其引起来。 可以通过包含多个**z**选项来一次打开多个转储文件，每个转储文件后跟不同的*DumpFile*值。 有关详细信息，请参阅[分析用户模式转储文件](analyzing-a-user-mode-dump-file.md)。

<span id="_______-zp_______PageFile______"></span><span id="_______-zp_______pagefile______"></span><span id="_______-ZP_______PAGEFILE______"></span>**-zp** *页面文件*   
指定已修改的页面文件的名称。 如果正在调试转储文件，并且想要使用[**pagein （内存中的页）**](-pagein--page-in-memory-.md)命令，此方法非常有用。 不能将 **-zp**与标准 Windows 页面文件一起使用，只能使用经过特别修改的页面文件。

<span id="_______executable______"></span><span id="_______EXECUTABLE______"></span>*可执行*   
指定可执行进程的命令行。 此操作用于启动新进程并对其进行调试。 这必须是命令行上的最后一项。 可执行文件名称后的所有文本都作为其参数字符串传递到可执行文件。

<span id="_______-_______"></span>**-?**   
显示命令行帮助文本。

从 "开始" 启动调试器 **|运行**或在命令提示符窗口中，在应用程序的文件名后指定目标应用程序的参数。 例如：

```dbgcmd
cdb myexe arg1arg2
```

 

 





