---
title: for_each_module
description: For_each_module 扩展对每个加载的模块执行一次调试器命令。
keywords:
- for_each_module Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- for_each_module
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 788bc9206d9d27ea30498968a900220c48e2a108
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815519"
---
# <a name="for_each_module"></a>！对于 \_ 每个 \_ 模块


对于每个模块扩展， **\_ 每个 \_ 模块** 扩展对每个加载的模块执行一次调试器命令。

```dbgcmd
!for_each_module ["CommandString"]
!for_each_module -?
```

## <a name="span-idddk__for_each_module_dbgspanspan-idddk__for_each_module_dbgspanparameters"></a><span id="ddk__for_each_module_dbg"></span><span id="DDK__FOR_EACH_MODULE_DBG"></span>参数


<span id="_______CommandString______"></span><span id="_______commandstring______"></span><span id="_______COMMANDSTRING______"></span>*Command.commandstring*   
指定为调试器的模块列表中的每个模块执行一次的调试器命令。 如果 *command.commandstring* 包含多个命令，则必须用分号分隔它们，并将 *command.commandstring* 括在引号中。 如果包含多个命令，则 *command.commandstring* 中的单个命令不能包含引号。

可以在 *command.commandstring* 或 *command.commandstring* 中的命令执行的任何脚本中使用以下别名。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Alias</th>
<th align="left">数据类型</th>
<th align="left">值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>@ #FileVersion</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>模块的文件版本。</p></td>
</tr>
<tr class="even">
<td align="left"><p>@ #ProductVersion</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>模块的产品版本。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>@ #ModuleIndex</p></td>
<td align="left"><p>ULONG</p></td>
<td align="left"><p>模块号。 模块是连续枚举的，从零开始。</p></td>
</tr>
<tr class="even">
<td align="left"><p>@ #ModuleName</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>模块名。 此名称通常是没有文件扩展名的文件名。 在某些情况下，模块名称与文件名明显不同。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>@ #ImageName</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>可执行文件的名称，包括文件扩展名。 通常，完整路径包含在用户模式下，而不是在内核模式下。</p></td>
</tr>
<tr class="even">
<td align="left"><p>@ #LoadedImageName</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>除非存在 Microsoft CodeView 符号，否则此别名与映像名称相同。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>@ #MappedImageName</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>在大多数情况下，此别名为 <strong>NULL</strong>。 如果调试器正在映射图像文件 (例如，在) 小型转储调试期间，此别名是映射映像的名称。</p></td>
</tr>
<tr class="even">
<td align="left"><p>@ #SymbolFileName</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>符号文件的路径和名称。 如果尚未加载任何符号，则此别名是可执行文件的名称。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>@ #ModuleNameSize</p></td>
<td align="left"><p>ULONG</p></td>
<td align="left"><p>模块名称字符串的字符串长度加1。</p></td>
</tr>
<tr class="even">
<td align="left"><p>@ #ImageNameSize</p></td>
<td align="left"><p>ULONG</p></td>
<td align="left"><p>映像名称字符串的字符串长度加1。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>@ #LoadedImageNameSize</p></td>
<td align="left"><p>ULONG</p></td>
<td align="left"><p>加载的映像名称字符串的字符串长度加1。</p></td>
</tr>
<tr class="even">
<td align="left"><p>@ #MappedImageNameSize</p></td>
<td align="left"><p>ULONG</p></td>
<td align="left"><p>映射的图像名称字符串的字符串长度加1。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>@ #SymbolFileNameSize</p></td>
<td align="left"><p>ULONG</p></td>
<td align="left"><p>符号文件名称字符串的字符串长度加一。</p></td>
</tr>
<tr class="even">
<td align="left"><p>@ #Base</p></td>
<td align="left"><p>ULONG64</p></td>
<td align="left"><p>图像开头的地址。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>@ #Size</p></td>
<td align="left"><p>ULONG</p></td>
<td align="left"><p>图像的大小（以字节为单位）。</p></td>
</tr>
<tr class="even">
<td align="left"><p>@ #End</p></td>
<td align="left"><p>ULONG64</p></td>
<td align="left"><p>图像末尾的地址。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>@ #TimeDateStamp</p></td>
<td align="left"><p>ULONG</p></td>
<td align="left"><p>图像的时间和日期戳。 如果要将此时间和日期戳扩展为可读的日期，请使用 <strong><a href="-formats--show-number-formats-.md" data-raw-source="[.formats (Show Number Formats)](-formats--show-number-formats-.md)">. 格式 (在) 命令中显示数字格式 </a></strong> 。</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>@ #Checksum</p></td>
<td align="left"><p>ULONG</p></td>
<td align="left"><p>模块的校验和。</p></td>
</tr>
<tr class="even">
<td align="left"><p>@ #Flags</p></td>
<td align="left"><p>ULONG</p></td>
<td align="left"><p>模块标志。 有关 DEBUG_MODULE_<em>Xxx</em> 值的列表，请参阅 Dbgeng。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>@ #SymbolType</p></td>
<td align="left"><p>USHORT</p></td>
<td align="left"><p>符号类型。 有关 DEBUG_SYMTYPE_<em>Xxx</em> 值的列表，请参阅 Dbgeng。</p></td>
</tr>
</tbody>
</table>

 

在对每个模块执行 *command.commandstring* 之前，以及在进行任何其他分析之前，将替换这些别名。 这些别名区分大小写。 必须在别名前面加上一个空格，后面加一个空格，即使别名括在括号中。 如果使用 c + + 表达式语法，则必须将这些别名作为 @ @ ( @ \# *alias*) 引用。

这些别名仅在对 **\_ 每个 \_ 模块** 调用的生存期内可用。 不要将它们与伪寄存器、固定名称别名或用户命名别名混淆。

<span id="_______-_______"></span> -?   
在 [调试器命令窗口](debugger-command-window.md)中显示此扩展的一些帮助文本。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Windows 2000</p></td>
<td align="left"><p>Ext.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows XP 及更高版本</p></td>
<td align="left"><p>Ext.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关如何定义和使用别名作为输入字符串的快捷方式的详细信息 (包括使用 $ {} token) ，请参阅 [使用别名](using-aliases.md)。

<a name="remarks"></a>备注
-------

如果未指定任何参数，则 **\_ 每个 \_ 模块** 扩展的！将显示有关已加载模块的一般信息。 此信息类似于以下命令所示的信息。

```dbgcmd
!for_each_module .echo @#ModuleIndex : @#Base @#End @#ModuleName @#ImageName  @#LoadedImageName
```

有关加载和卸载的模块的详细信息，请使用 " [**lm (List)**](lm--list-loaded-modules-.md) 命令"。

如果启用 "详细调试器输出"，调试器将在调用扩展时显示加载和卸载的模块的总数，并且调试器显示每个模块 (的详细信息，包括在对该模块执行 *command.commandstring* 之前) 每个可用别名的值。

下面的示例演示如何将 **！用于 \_ 每个 \_ 模块** 扩展。 以下命令显示全局调试标志。

```dbgcmd
!for_each_module x ${@#ModuleName}!*Debug*Flag*
!for_each_module x ${@#ModuleName}!g*Debug*
```

以下命令使用 [**！ chkimg**](-chkimg.md) extension 检查每个加载的模块中是否存在二进制损坏：

```dbgcmd
!for_each_module !chkimg @#ModuleName
```

以下命令在每个加载的映像中搜索模式 "MZ"。

```dbgcmd
!for_each_module s-a @#Base @#End "MZ"
```

下面的示例演示如何将 @ \# FileVersion 和 @ \# ProductVersion 用于每个模块名称：

```dbgcmd
0:000> !for_each_module .echo @#ModuleName fver = @#FileVersion pver = @#ProductVersion 
USER32 fver = 6.0.6000.16438 (vista_gdr.070214-1610) pver = 6.0.6000.16438
kernel32 fver = 6.0.6000.16386 (vista_rtm.061101-2205) pver = 6.0.6000.16386
ntdll fver = 6.0.6000.16386 (vista_rtm.061101-2205) pver = 6.0.6000.16386
notepad fver = 6.0.6000.16386 (vista_rtm.061101-2205) pver = 6.0.6000.16386
WINSPOOL fver = 6.0.6000.16386 (vista_rtm.061101-2205) pver = 6.0.6000.16386
COMCTL32 fver = 6.10 (vista_rtm.061101-2205) pver = 6.0.6000.16386
SHLWAPI fver = 6.0.6000.16386 (vista_rtm.061101-2205) pver = 6.0.6000.16386
msvcrt fver = 7.0.6000.16386 (vista_rtm.061101-2205) pver = 7.0.6000.16386
GDI32 fver = 6.0.6000.16386 (vista_rtm.061101-2205) pver = 6.0.6000.16386
RPCRT4 fver = 6.0.6000.16525 (vista_gdr.070716-1600) pver = 6.0.6000.16525
SHELL32 fver = 6.0.6000.16513 (vista_gdr.070626-1505) pver = 6.0.6000.16513
ole32 fver = 6.0.6000.16386 (vista_rtm.061101-2205) pver = 6.0.6000.16386
ADVAPI32 fver = 6.0.6000.16386 (vista_rtm.061101-2205) pver = 6.0.6000.16386
COMDLG32 fver = 6.0.6000.16386 (vista_rtm.061101-2205) pver = 6.0.6000.16386
```

 

 





