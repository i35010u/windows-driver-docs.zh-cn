---
title: 配置 tools.ini
description: 配置 tools.ini
keywords:
- tools.ini 文件
- ntsd.ini 文件
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9773f4b22b17d3058230885db77f787d70f9ac32
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823481"
---
# <a name="configuring-toolsini"></a>配置 tools.ini


## <span id="ddk_configuring_tools_ini_dbg"></span><span id="DDK_CONFIGURING_TOOLS_INI_DBG"></span>


文件 tools.ini 包含用于初始化命令行调试程序的信息。 启动时，调试器会在 tools.ini 文件中搜索相应的节标头，并从标头下的条目中提取初始化信息。 每个命令行调试程序都有自己的节标头- \[ CDB \] 、 \[ NTSD \] 和 \[ KD \] 。 环境变量 INIT 必须指向包含 tools.ini 文件的目录。

WinDbg 不使用 tools.ini 文件。 而是在 [工作区](using-workspaces.md)中保存初始化设置。

下表显示了 tools.ini 项。

关键字必须与值之间用空格或冒号分隔。 关键字不区分大小写。

对于 **TRUE** 或 **FALSE** 值，"false" 是唯一的 false 值。 任何其他情况均为 **TRUE**。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">条目</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>$u 0：</strong> <em>值</em> .。。 <strong>$u 9：</strong> <em>值</em></p></td>
<td align="left"><p>为固定名称的别名赋值。 可以指定数值 <em>n</em> 或 <em>0xn</em> 或任何其他字符串。 有关详细信息，请参阅 <a href="using-aliases.md" data-raw-source="[Using Aliases](using-aliases.md)">使用别名</a> 。 无命令行等效项。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>DebugChildren：</strong> <em>标志</em></p></td>
<td align="left"><p><strong>TRUE</strong> 或 <strong>FALSE</strong>。 如果 <strong>为 TRUE</strong>，则 CDB 将调试指定的应用程序以及它可能生成的任何子进程。 等效命令行： <strong>-o</strong>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>DebugOutput：</strong> <em>标志</em></p></td>
<td align="left"><p><strong>TRUE</strong> 或 <strong>FALSE</strong>。 如果 <strong>为 TRUE，则</strong>CDB 发送输出，并通过终端接收输入。 如果 <strong>为 FALSE</strong>，则输出将进入用户屏幕。 命令行选项 <strong>-d</strong> 类似，但不完全相同。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>IniFile：</strong> <em>文件</em></p></td>
<td align="left"><p>指定 CDB 或 KD 在启动时执行命令的脚本文件的名称。 默认值为当前目录中的 ntsd.ini 文件。 等效的命令行是 <strong>-cf</strong>。有关详细信息，请参阅 <a href="using-script-files.md" data-raw-source="[Using Script Files](using-script-files.md)">使用脚本文件</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>LazyLoad：</strong> <em>标志</em></p></td>
<td align="left"><p><strong>TRUE</strong> 或 <strong>FALSE</strong>。 如果 <strong>为 TRUE</strong>，则 CDB 执行延迟符号加载;也就是说，除非需要，否则不会加载符号。 等效的命令行为 <strong>-s</strong>。</p>
<p>有关详细信息以及设置此选项的其他方法，请参阅 <a href="deferred-symbol-loading.md" data-raw-source="[Deferred Symbol Loading](deferred-symbol-loading.md)">延迟符号加载</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>SetDll：</strong> <em>文件名</em></p></td>
<td align="left"><p>设置扩展 DLL。 应省略 .dll 文件扩展名。 默认值为 userexts.dll。 等效命令行为 <strong>-a</strong>。</p>
<p>有关详细信息和设置此默认设置的其他方法，请参阅 <a href="loading-debugger-extension-dlls.md" data-raw-source="[Loading Debugger Extension DLLs](loading-debugger-extension-dlls.md)">加载调试器扩展 dll</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>StopFirst：</strong> <em>标志</em></p></td>
<td align="left"><p><strong>TRUE</strong> 或 <strong>FALSE</strong>。 如果 <strong>为 true</strong>，则在图像加载过程结束时，CDB 会在断点处停止。 等效的命令行为 <strong>-g</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>StopOnProcessExit：</strong> <em>标志</em></p></td>
<td align="left"><p><strong>TRUE</strong> 或 <strong>FALSE</strong>。 如果 <strong>为 TRUE</strong>，则当 CDB 收到进程终止通知时，它将停止。 等效的命令行为 <strong>-G</strong>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p></p>
<strong>sxd：</strong> <em>event</em>
<strong>sxe：</strong> <em>事件</em></td>
<td align="left"><p>为指定的异常或事件设置调试器响应和处理状态。</p>
<p>可以通过以下方式指定异常和事件：</p>
<p></p>
<strong>*</strong>：默认异常 <em>n</em>：异常 <em>n</em> (decimal) <em>0xn</em>： exception <em>0xn</em> (十六进制)  (其他) ：事件代码
<p>有关此过程的详细信息以及其他控制这些设置的方法，请参阅 <a href="controlling-exceptions-and-events.md" data-raw-source="[Controlling Exceptions and Events](controlling-exceptions-and-events.md)">控制异常和事件</a> 。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>VerboseOutput：</strong> <em>标志</em></p></td>
<td align="left"><p><strong>TRUE</strong> 或 <strong>FALSE</strong>。 如果 <strong>为 TRUE</strong>，则 CDB 将显示有关符号处理、事件通知以及其他运行时匹配项的详细信息。 等效命令行： <strong>v</strong>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>行：</strong> <em>标志</em></p></td>
<td align="left"><p><strong>TRUE</strong> 或 <strong>FALSE</strong>。 行标志启用或禁用对源行信息的支持。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>srcopt：</strong> <em>选项</em></p></td>
<td align="left"><p>设置控制源显示和程序单步执行选项的源行选项。 有关详细信息，请参阅 <strong><a href="l---l---set-source-options-.md" data-raw-source="[l+, l- (Set Source Options)](l---l---set-source-options-.md)">l +，左 (设置源选项) </a></strong>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>srcpath：</strong> <em>目录</em></p></td>
<td align="left"><p>设置源文件搜索路径。 有关详细信息，请参阅 <strong><a href="-srcpath---lsrcpath--set-source-path-.md" data-raw-source="[.srcpath, .lsrcpath (Set Source Path)](-srcpath---lsrcpath--set-source-path-.md)">. srcpath、. lsrcpath (设置源路径) </a></strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>enable_unicode：</strong> <em>标志</em></p></td>
<td align="left"><p><strong>TRUE</strong> 或 <strong>FALSE</strong>。 Enable_unicode 标志指定调试器是否将 USHORT 指针和数组显示为 Unicode 字符串。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>force_radix_output：</strong> <em>标志</em></p></td>
<td align="left"><p><strong>TRUE</strong> 或 <strong>FALSE</strong>。 Force_radix_output 标志指定是以十进制格式还是在默认基数中显示整数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>col_mode：</strong> <em>标志</em></p></td>
<td align="left"><p><strong>TRUE</strong> 或 <strong>FALSE</strong>。 Col_mode 标志控制颜色模式设置。 启用颜色模式后，调试器可以生成彩色输出。 默认情况下，不会设置大多数颜色，而是默认设置为当前控制台颜色。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>col：</strong> <em>name</em> <em>colspec</em></p></td>
<td align="left"><p>该 <em>名称</em> 指示您要着色的元素。 <em>Colspec</em>是一个由三个字母组成的 RGB 指示器，其形式为 [rR-] [gG-] [bB-]。 小写字母表示较暗，大写字母表示较亮，短划线表示没有颜色组成部分。 由于控制台颜色限制，鲜艳并不真正按组件，而是在任何请求鲜时适用于所有组件。 换言之，rgB 与 RGB 相同。 出于此原因，如果要使用任何大写字母，则建议使用所有大写。</p>
<p>用法示例：</p>
<p>col： emphfg R--</p></td>
</tr>
</tbody>
</table>

 

下面是 \[ \] tools.ini 文件中的一个 NTSD 部分示例：

```inf
[NTSD]
sxe: 3c
sxe: cc
$u0: VeryLongName
VerboseOutput:true
```

 

 





