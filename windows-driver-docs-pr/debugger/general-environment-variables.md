---
title: 常规环境变量
description: 常规环境变量
ms.assetid: 1f37de92-0c62-4317-b3c6-24b3efd9b3b3
keywords:
- 环境变量常规
- _NO_DEBUG_HEAP 环境变量
- _NT_ALT_SYMBOL_PATH 环境变量
- _NT_DEBUG_HISTORY_SIZE 环境变量
- _NT_DEBUG_LOG_FILE_APPEND 环境变量
- _NT_DEBUG_LOG_FILE_OPEN 环境变量
- _NT_DEBUGGER_EXTENSION_PATH 环境变量
- _NT_EXECUTABLE_IMAGE_PATH environment variable
- _NT_SOURCE_PATH 环境变量
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 04adc9364db52af5579676fa1da57524c38fe799
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347100"
---
# <a name="general-environment-variables"></a>常规环境变量


## <span id="ddk_general_environment_variables_dbg"></span><span id="DDK_GENERAL_ENVIRONMENT_VARIABLES_DBG"></span>


下表列出了可在用户模式和内核模式调试的环境变量。

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
<td align="left"><p>_NT_DEBUGGER_EXTENSION_PATH = <em>Path</em></p></td>
<td align="left"><p>指定调试器将先搜索扩展 Dll 的路径。 <em>路径</em>可以包含驱动器号后, 接一个冒号 (<strong>:</strong>)。 用分号分隔多个目录 (<strong>;</strong>)。 有关详细信息，请参阅<a href="loading-debugger-extension-dlls.md" data-raw-source="[Loading Debugger Extension DLLs](loading-debugger-extension-dlls.md)">加载的调试器扩展 Dll</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>_NT_EXECUTABLE_IMAGE_PATH = <em>Path</em></p></td>
<td align="left"><p>指定包含二进制可执行文件的路径。 <em>路径</em>可以包含驱动器号后, 接一个冒号 (<strong>:</strong>)。 用分号分隔多个目录 (<strong>;</strong>)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>_NT_SOURCE_PATH = <em>Path</em></p></td>
<td align="left"><p>指定包含目标的源代码文件的路径。 <em>路径</em>可以包含驱动器号后, 接一个冒号 (<strong>:</strong>)。 用分号分隔多个目录 (<strong>;</strong>)。 有关详细信息，以及更改此路径的其他方法，请参阅<a href="source-path.md" data-raw-source="[Source Path](source-path.md)">源路径</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>_NT_SYMBOL_PATH = <em>Path</em></p></td>
<td align="left"><p>指定包含符号文件的目录树的根。 <em>路径</em>可以包含驱动器号后, 接一个冒号 (<strong>:</strong>)。 用分号分隔多个目录 (<strong>;</strong>)。 有关详细信息，以及更改此路径的其他方法，请参阅<a href="symbol-path.md" data-raw-source="[Symbol Path](symbol-path.md)">符号路径</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>_NT_ALT_SYMBOL_PATH = <em>Path</em></p></td>
<td align="left"><p>指定搜索之前 _NT_SYMBOL_PATH 替代符号路径。 这可用于保留符号文件的专用版本。 <em>路径</em>可以包含驱动器号后, 接一个冒号 (<strong>:</strong>)。 用分号分隔多个目录 (<strong>;</strong>)。 有关详细信息，请参阅<a href="symbol-path.md" data-raw-source="[Symbol Path](symbol-path.md)">符号路径</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>_NT_SYMBOL_PROXY =<em>代理</em><strong>:</strong><em>端口</em></p></td>
<td align="left"><p>指定要由 SymSrv 的代理服务器。 有关详细信息，请参阅<a href="firewalls-and-proxy-servers.md" data-raw-source="[Firewalls and Proxy Servers](firewalls-and-proxy-servers.md)">防火墙和代理服务器</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>_NT_DEBUG_HISTORY_SIZE = <em>Number</em></p></td>
<td align="left"><p>可以在远程调试过程中访问的命令历史记录中指定命令的数。 命令的长度会有所不同，因为可用的行数可能不完全匹配<em>数</em>。 有关详细信息，以及更改此数字的其他方法，请参阅<a href="using-debugger-commands.md" data-raw-source="[Using Debugger Commands](using-debugger-commands.md)">使用调试器命令</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>_NT_DEBUG_LOG_FILE_OPEN = <em>Filename</em></p></td>
<td align="left"><p>（CDB 和仅 KD）指定调试程序应向其发送输出的日志文件。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>_NT_DEBUG_LOG_FILE_APPEND = <em>Filename</em></p></td>
<td align="left"><p>（CDB 和仅 KD）指定调试器应将输出追加到日志文件。</p></td>
</tr>
<tr class="even">
<td align="left"><p>_NT_EXPR_EVAL = {<strong>masm</strong> | <strong>c++</strong>}</p></td>
<td align="left"><p>指定默认表达式计算器。 如果<strong>masm</strong>指定，则将使用 MASM 表达式语法。 如果<strong>c + +</strong>指定，则C++将使用表达式语法。 默认值为 MASM 表达式语法。 请参阅<a href="evaluating-expressions.md" data-raw-source="[Evaluating Expressions](evaluating-expressions.md)">评估表达式</a>有关详细信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>_NO_DEBUG_HEAP</p></td>
<td align="left"><p>指定调试堆不应使用用户模式调试。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBGENG_NO_DEBUG_PRIVILEGE</p></td>
<td align="left"><p>可防止生成继承 SeDebugPrivilege 调试器的进程。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBGENG_NO_BUGCHECK_ANALYSIS</p></td>
<td align="left"><p>防止自动检测错误分析。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBGHELP_HOMEDIR</p></td>
<td align="left"><p>指定由 SymSrv 和 SrcSrv 默认下游 store 的根目录的路径。 <em>路径</em>可以包含驱动器号后, 接一个冒号 (<strong>:</strong>)。 用分号分隔多个目录 (<strong>;</strong>)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SRCSRV_INI_FILE</p></td>
<td align="left"><p>指定的路径和名称使用的配置文件<a href="srcsrv.md" data-raw-source="[SrcSrv](srcsrv.md)">SrcSrv</a>。 默认情况下，路径是有关 Windows 调试工具安装目录的 srcsrv 子目录和文件名称是 Srcsrv.ini。 请参阅<a href="source-indexing.md" data-raw-source="[Source Indexing](source-indexing.md)">源索引编制</a>有关详细信息。</p></td>
</tr>
</tbody>
</table>

 

 

 





