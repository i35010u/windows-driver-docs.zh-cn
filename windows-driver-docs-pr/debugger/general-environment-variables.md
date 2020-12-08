---
title: 常规环境变量
description: 常规环境变量
keywords:
- 环境变量，常规
- _NO_DEBUG_HEAP 环境变量
- _NT_ALT_SYMBOL_PATH 环境变量
- _NT_DEBUG_HISTORY_SIZE 环境变量
- _NT_DEBUG_LOG_FILE_APPEND 环境变量
- _NT_DEBUG_LOG_FILE_OPEN 环境变量
- _NT_DEBUGGER_EXTENSION_PATH 环境变量
- _NT_EXECUTABLE_IMAGE_PATH 环境变量
- _NT_SOURCE_PATH 环境变量
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: cd7bca9c19f413ff0fd1fdf56b2b12ba0a245bd0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96787785"
---
# <a name="general-environment-variables"></a>常规环境变量


## <span id="ddk_general_environment_variables_dbg"></span><span id="DDK_GENERAL_ENVIRONMENT_VARIABLES_DBG"></span>


下表列出了可在用户模式和内核模式调试中使用的环境变量。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">变量</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>_NT_DEBUGGER_EXTENSION_PATH = <em>路径</em></p></td>
<td align="left"><p>指定调试器将首先搜索扩展 Dll 的路径。 <em>路径</em> 可以包含后跟冒号 (<strong>：</strong>) 的驱动器号。 用分号 (<strong>;</strong>) 分隔多个目录。 有关详细信息，请参阅 <a href="loading-debugger-extension-dlls.md" data-raw-source="[Loading Debugger Extension DLLs](loading-debugger-extension-dlls.md)">加载调试器扩展 dll</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>_NT_EXECUTABLE_IMAGE_PATH = <em>路径</em></p></td>
<td align="left"><p>指定包含二进制可执行文件的路径。 <em>路径</em> 可以包含后跟冒号 (<strong>：</strong>) 的驱动器号。 用分号 (<strong>;</strong>) 分隔多个目录。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>_NT_SOURCE_PATH = <em>路径</em></p></td>
<td align="left"><p>指定包含目标的源文件的路径。 <em>路径</em> 可以包含后跟冒号 (<strong>：</strong>) 的驱动器号。 用分号 (<strong>;</strong>) 分隔多个目录。 有关详细信息，请参阅 <a href="source-path.md" data-raw-source="[Source Path](source-path.md)">源路径</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>_NT_SYMBOL_PATH = <em>路径</em></p></td>
<td align="left"><p>指定包含符号文件的目录树的根。 <em>路径</em> 可以包含后跟冒号 (<strong>：</strong>) 的驱动器号。 用分号 (<strong>;</strong>) 分隔多个目录。 有关详细信息和更改此路径的其他方式，请参阅 <a href="symbol-path.md" data-raw-source="[Symbol Path](symbol-path.md)">符号路径</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>_NT_ALT_SYMBOL_PATH = <em>路径</em></p></td>
<td align="left"><p>指定 _NT_SYMBOL_PATH 之前搜索的备用符号路径。 这对于保存符号文件的私有版本非常有用。 <em>路径</em> 可以包含后跟冒号 (<strong>：</strong>) 的驱动器号。 用分号 (<strong>;</strong>) 分隔多个目录。 有关详细信息，请参阅 <a href="symbol-path.md" data-raw-source="[Symbol Path](symbol-path.md)">符号路径</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>_NT_SYMBOL_PROXY = <em>PROXY</em><strong>：</strong><em>端口</em></p></td>
<td align="left"><p>指定 SymSrv 要使用的代理服务器。 有关详细信息，请参阅 <a href="firewalls-and-proxy-servers.md" data-raw-source="[Firewalls and Proxy Servers](firewalls-and-proxy-servers.md)">防火墙和代理服务器</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>_NT_DEBUG_HISTORY_SIZE = <em>Number</em></p></td>
<td align="left"><p>指定在远程调试过程中可以访问的命令历史记录中的命令数。 由于命令的长度不同，可用的行数可能与 <em>数字</em>不完全匹配。 有关详细信息以及其他更改此数字的方法，请参阅 <a href="using-debugger-commands.md" data-raw-source="[Using Debugger Commands](using-debugger-commands.md)">使用调试器命令</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>_NT_DEBUG_LOG_FILE_OPEN = <em>Filename</em></p></td>
<td align="left"><p> (CDB 和 KD 仅) 指定调试程序应将输出发送到的日志文件。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>_NT_DEBUG_LOG_FILE_APPEND = <em>Filename</em></p></td>
<td align="left"><p> (CDB 和 KD 仅) 指定调试器应将输出追加到的日志文件。</p></td>
</tr>
<tr class="even">
<td align="left"><p>_NT_EXPR_EVAL = {<strong>masm</strong>  |  <strong>c + +</strong>}</p></td>
<td align="left"><p>指定默认表达式计算器。 如果指定了 <strong>masm</strong> ，将使用 masm 表达式语法。 如果指定 <strong>c + +</strong> ，将使用 c + + 表达式语法。 MASM expression 语法为默认值。 有关详细信息，请参阅 <a href="evaluating-expressions.md" data-raw-source="[Evaluating Expressions](evaluating-expressions.md)">计算表达式</a> 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>_NO_DEBUG_HEAP</p></td>
<td align="left"><p>指定调试堆不应用于用户模式调试。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBGENG_NO_DEBUG_PRIVILEGE</p></td>
<td align="left"><p>阻止调试器生成的进程继承 SeDebugPrivilege。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBGENG_NO_BUGCHECK_ANALYSIS</p></td>
<td align="left"><p>阻止自动检测错误。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBGHELP_HOMEDIR</p></td>
<td align="left"><p>指定由 SymSrv 和 Srcsrv.ini 使用的默认下游存储区的根路径。 <em>路径</em> 可以包含后跟冒号 (<strong>：</strong>) 的驱动器号。 用分号 (<strong>;</strong>) 分隔多个目录。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SRCSRV_INI_FILE</p></td>
<td align="left"><p>指定 <a href="srcsrv.md" data-raw-source="[SrcSrv](srcsrv.md)">srcsrv.ini</a>使用的配置文件的路径和名称。 默认情况下，该路径是适用于 Windows 的调试工具安装目录的 srcsrv.ini 子目录，文件名为 Srcsrv.ini。 有关详细信息，请参阅 <a href="source-indexing.md" data-raw-source="[Source Indexing](source-indexing.md)">源索引</a> 。</p></td>
</tr>
</tbody>
</table>

 

 

 





