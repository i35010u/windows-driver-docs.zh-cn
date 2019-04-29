---
title: 配置 tools.ini
description: 配置 tools.ini
ms.assetid: 4f0d9f48-99d5-4180-b25d-70fd8de6f20e
keywords:
- tools.ini 文件
- ntsd.ini 文件
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 82c07d43844c941446d93c6646615dc42e84e63d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375063"
---
# <a name="configuring-toolsini"></a>配置 tools.ini


## <span id="ddk_configuring_tools_ini_dbg"></span><span id="DDK_CONFIGURING_TOOLS_INI_DBG"></span>


文件 tools.ini 包含初始化命令行调试器的信息。 在启动时，调试器搜索 tools.ini 文件中的相应部分标头，并从标头下的条目中提取的初始化信息。 每个命令行调试程序具有其自己的部分标头- \[CDB\]， \[NTSD\]，并\[KD\]。 环境变量 INIT 必须指向包含 tools.ini 文件的目录。

WinDbg 不使用 tools.ini 文件。 相反，WinDbg 将保存在初始化设置[工作区](using-workspaces.md)。

Tools.ini 条目表所示。

关键字必须由空格或冒号分隔的值。 关键字不区分大小写。

有关 **，则返回 TRUE**或**FALSE** "FALSE"的值是仅 false 值。 其他任何内容是 **，则返回 TRUE**。

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
<td align="left"><p><strong>$u0:</strong> <em>值</em>...<strong>美元 u9:</strong> <em>值</em></p></td>
<td align="left"><p>将值分配给固定名称的别名。 可以指定数值<em>n</em>或<em>0xn</em>或任何其他字符串。 请参阅<a href="using-aliases.md" data-raw-source="[Using Aliases](using-aliases.md)">Using 别名</a>有关详细信息。 没有命令行等效项。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>DebugChildren:</strong> <em>标志</em></p></td>
<td align="left"><p><strong>TRUE</strong>或<strong>FALSE</strong>。 如果<strong>，则返回 TRUE</strong>，CDB 调试指定的应用程序，以及它可能会生成任何子进程。 命令行等效项是<strong>-o</strong>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>DebugOutput:</strong> <em>标志</em></p></td>
<td align="left"><p><strong>TRUE</strong>或<strong>FALSE</strong>。 如果<strong>，则返回 TRUE</strong>，CDB 将输出发送和接收通过终端输入。 如果<strong>FALSE</strong>，输出会转至用户屏幕。 命令行选项<strong>-d</strong>类似，但不完全相同。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>IniFile:</strong> <em>文件</em></p></td>
<td align="left"><p>指定的 CDB 或 KD 中的命令需要启动的脚本文件的名称。 默认值为当前目录中的 ntsd.ini 文件。 命令行等效项是<strong>-cf</strong>。有关详细信息，请参阅<a href="using-script-files.md" data-raw-source="[Using Script Files](using-script-files.md)">使用脚本文件</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>LazyLoad:</strong> <em>标志</em></p></td>
<td align="left"><p><strong>TRUE</strong>或<strong>FALSE</strong>。 如果<strong>，则返回 TRUE</strong>，CDB 执行延迟的符号加载; 也就是说，还未加载符号之前所需。 命令行等效项是<strong>-s</strong>。</p>
<p>有关详细信息，并将此选项设置的其他方法，请参阅<a href="deferred-symbol-loading.md" data-raw-source="[Deferred Symbol Loading](deferred-symbol-loading.md)">延迟的符号加载</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>SetDll:</strong> <em>文件名</em></p></td>
<td align="left"><p>设置扩展 DLL。 应省略.dll 文件扩展名。 默认值为 userexts.dll。 命令行等效项是<strong>-a</strong>。</p>
<p>有关详细信息，并设置此默认设置的其他方法，请参阅<a href="loading-debugger-extension-dlls.md" data-raw-source="[Loading Debugger Extension DLLs](loading-debugger-extension-dlls.md)">加载的调试器扩展 Dll</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>StopFirst:</strong> <em>标志</em></p></td>
<td align="left"><p><strong>TRUE</strong>或<strong>FALSE</strong>。 如果<strong>，则返回 true</strong>，CDB 末尾的图像加载过程在断点处停止。 命令行等效项是<strong>-g</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>StopOnProcessExit:</strong> <em>标志</em></p></td>
<td align="left"><p><strong>TRUE</strong>或<strong>FALSE</strong>。 如果<strong>，则返回 TRUE</strong>，CDB 停止接收进程终止通知时。 命令行等效项是<strong>-G</strong>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p></p>
<strong>sxd:</strong> <em>event</em>
<strong>sxe:</strong> <em>event</em></td>
<td align="left"><p>设置调试器响应和指定的异常或事件的处理状态。</p>
<p>异常和事件可能按以下方式指定：</p>
<p></p>
<strong>*</strong>:默认异常<em>n</em>:异常<em>n</em> (decimal) <em>0xn</em>:异常<em>0xn</em> （十六进制） （其他）：事件代码
<p>请参阅<a href="controlling-exceptions-and-events.md" data-raw-source="[Controlling Exceptions and Events](controlling-exceptions-and-events.md)">控制异常和事件</a>为此过程的详细信息和控制这些设置的其他方法。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>VerboseOutput:</strong> <em>标志</em></p></td>
<td align="left"><p><strong>TRUE</strong>或<strong>FALSE</strong>。 如果<strong>，则返回 TRUE</strong>，CDB 会显示有关符号处理、 事件通知和其他运行时匹配项的详细的信息。 命令行等效项是<strong>-v</strong>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>行：</strong> <em>标志</em></p></td>
<td align="left"><p><strong>TRUE</strong>或<strong>FALSE</strong>。 行标志启用或禁用对源行信息的支持。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>srcopt:</strong> <em>选项</em></p></td>
<td align="left"><p>设置源行选项，控制源显示和单步执行选项的程序。 有关详细信息请参阅 <strong><a href="l---l---set-source-options-.md" data-raw-source="[l+, l- (Set Source Options)](l---l---set-source-options-.md)">l +，l-（设置源选项）</a></strong>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>srcpath:</strong> <em>directory</em></p></td>
<td align="left"><p>设置源文件搜索路径。 有关详细信息请参阅 <strong><a href="-srcpath---lsrcpath--set-source-path-.md" data-raw-source="[.srcpath, .lsrcpath (Set Source Path)](-srcpath---lsrcpath--set-source-path-.md)">.srcpath，.lsrcpath （设置源路径）</a></strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>enable_unicode:</strong> <em>flag</em></p></td>
<td align="left"><p><strong>TRUE</strong>或<strong>FALSE</strong>。 Enable_unicode 标志指定调试器为 Unicode 字符串是否显示 USHORT 指针和数组。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>force_radix_output:</strong> <em>flag</em></p></td>
<td align="left"><p><strong>TRUE</strong>或<strong>FALSE</strong>。 Force_radix_output 标志指定是否显示整数十进制格式或默认基数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>col_mode:</strong> <em>标志</em></p></td>
<td align="left"><p><strong>TRUE</strong>或<strong>FALSE</strong>。 Col_mode 标志控制颜色模式设置。 启用颜色模式调试器可以生成彩色的输出。 默认情况下，大多数颜色未设置，而是默认为当前控制台颜色。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>col:</strong> <em>name</em> <em>colspec</em></p></td>
<td align="left"><p><em>名称</em>指示着色的元素。 <em>Colspec</em>是窗体 [rR-] [gG-] [bB-] 的三个字母 RGB 指示器。 小写字母指示较深，大写字母表示 brighter，短划线表示没有颜色组件的发布内容。 由于控制台颜色的限制，亮不实际上每个组件，但如果有任何亮请求适用于所有组件。 换而言之，rgB 是 RGB 相同。 出于此原因，建议，如果打算使用任何 caps 使用全部大写。</p>
<p>示例用法：</p>
<p>列号： emphfg R-</p></td>
</tr>
</tbody>
</table>

 

一个示例\[NTSD\] tools.ini 文件中的部分将跟踪：

```inf
[NTSD]
sxe: 3c
sxe: cc
$u0: VeryLongName
VerboseOutput:true
```

 

 





