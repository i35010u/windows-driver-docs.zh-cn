---
title: for_each_module
description: For_each_module 扩展执行调试器命令一次为每个加载的模块。
ms.assetid: 607947d8-be06-4012-8901-13bf27e382b1
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
ms.openlocfilehash: 4455402ce1b2b061449c54cad58983e89077f7b3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336634"
---
# <a name="foreachmodule"></a>!for\_each\_module


**！ 有关\_每个\_模块**扩展执行一次为每个已加载模块的调试器命令。

```dbgcmd
!for_each_module ["CommandString"]
!for_each_module -?
```

## <a name="span-idddkforeachmoduledbgspanspan-idddkforeachmoduledbgspanparameters"></a><span id="ddk__for_each_module_dbg"></span><span id="DDK__FOR_EACH_MODULE_DBG"></span>参数


<span id="_______CommandString______"></span><span id="_______commandstring______"></span><span id="_______COMMANDSTRING______"></span> *CommandString*   
指定要为执行一次每个模块的调试程序的模块列表中的调试器命令。 如果*CommandString*包括多个命令，必须使用分号分隔并括起来*CommandString*引号引起来。 如果包含多个命令，对单个命令中*CommandString*不能包含引号引起来。

可以使用中的以下别名*CommandString*或任意脚本中的命令*CommandString*执行。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">别名</th>
<th align="left">数据类型</th>
<th align="left">值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>@#FileVersion</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>文件版本的模块。</p></td>
</tr>
<tr class="even">
<td align="left"><p>@#ProductVersion</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>模块的产品版本。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>@#ModuleIndex</p></td>
<td align="left"><p>ULONG</p></td>
<td align="left"><p>模块数。 从零开始，模块将连续，枚举。</p></td>
</tr>
<tr class="even">
<td align="left"><p>@#ModuleName</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>模块名称。 此名称通常是不带文件扩展名的文件名称。 在某些情况下，模块名称明显不同于的文件的名称。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>@#ImageName</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>可执行文件，其中包括文件扩展名的名称。 通常情况下，完整路径是包含在用户模式下，但不是在内核模式下。</p></td>
</tr>
<tr class="even">
<td align="left"><p>@#LoadedImageName</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>除非存在 Microsoft CodeView 符号时，此别名是映像名称不同。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>@#MappedImageName</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>在大多数情况下，此别名是<strong>NULL</strong>。 如果调试器 （例如，小型转储调试期间），映射的图像文件，此别名是映像的映射的名称。</p></td>
</tr>
<tr class="even">
<td align="left"><p>@#SymbolFileName</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>路径和符号文件的名称。 如果还未加载任何符号，此别名是可执行文件的名称。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>@#ModuleNameSize</p></td>
<td align="left"><p>ULONG</p></td>
<td align="left"><p>字符串长度的模块名称字符串，加 1。</p></td>
</tr>
<tr class="even">
<td align="left"><p>@#ImageNameSize</p></td>
<td align="left"><p>ULONG</p></td>
<td align="left"><p>字符串长度的映像名称字符串，加 1。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>@#LoadedImageNameSize</p></td>
<td align="left"><p>ULONG</p></td>
<td align="left"><p>加载的映像名称字符串，以及一个字符串长度。</p></td>
</tr>
<tr class="even">
<td align="left"><p>@#MappedImageNameSize</p></td>
<td align="left"><p>ULONG</p></td>
<td align="left"><p>字符串长度的映射的图像名称字符串，加 1。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>@#SymbolFileNameSize</p></td>
<td align="left"><p>ULONG</p></td>
<td align="left"><p>字符串长度的符号文件名称字符串，加 1。</p></td>
</tr>
<tr class="even">
<td align="left"><p>@#Base</p></td>
<td align="left"><p>ULONG64</p></td>
<td align="left"><p>图像的起始地址。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>@#Size</p></td>
<td align="left"><p>ULONG</p></td>
<td align="left"><p>图像，以字节为单位的大小。</p></td>
</tr>
<tr class="even">
<td align="left"><p>@#End</p></td>
<td align="left"><p>ULONG64</p></td>
<td align="left"><p>映像的端的地址。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>@#TimeDateStamp</p></td>
<td align="left"><p>ULONG</p></td>
<td align="left"><p>图像的时间和日期戳。 如果你想要展开此日期和时间戳转换为可读的日期，使用<strong><a href="-formats--show-number-formats-.md" data-raw-source="[.formats (Show Number Formats)](-formats--show-number-formats-.md)">（显示数字格式） 的.formats</a></strong>命令。</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>@#Checksum</p></td>
<td align="left"><p>ULONG</p></td>
<td align="left"><p>模块的校验和。</p></td>
</tr>
<tr class="even">
<td align="left"><p>@#Flags</p></td>
<td align="left"><p>ULONG</p></td>
<td align="left"><p>模块的标志。 有关一系列 DEBUG_MODULE_<em>Xxx</em>值，请参阅 Dbgeng.h。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>@#SymbolType</p></td>
<td align="left"><p>USHORT</p></td>
<td align="left"><p>符号类型。 有关一系列 DEBUG_SYMTYPE_<em>Xxx</em>值，请参阅 Dbgeng.h。</p></td>
</tr>
</tbody>
</table>

 

这些别名会替换之前*CommandString*为每个模块和任何其他分析发生之前执行。 这些别名是区分大小写。 必须添加别名之前的空格和一个空格后，即使该别名括在括号中。 如果使用C++表达式语法，必须引用作为这些别名 @ @ (@\#*别名*)。

这些别名对调用的生存期内仅有 **！ 有关\_每个\_模块**。 不要混淆它们使用伪寄存器、 固定名称的别名或用户命名别名。

<span id="_______-_______"></span> -?   
显示此扩展中的一些帮助文本[调试器命令窗口](debugger-command-window.md)。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

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

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关如何定义和别名用作快捷方式的输入字符串 （包括使用 $ {} 令牌） 的详细信息，请参阅[Using 别名](using-aliases.md)。

<a name="remarks"></a>备注
-------

如果未指定任何参数， **！ 有关\_每个\_模块**扩展显示有关已加载模块的常规信息。 此信息是类似于下面的命令显示的信息。

```dbgcmd
!for_each_module .echo @#ModuleIndex : @#Base @#End @#ModuleName @#ImageName  @#LoadedImageName
```

有关详细信息大约加载和卸载的模块，使用[ **lm （列表加载模块）** ](lm--list-loaded-modules-.md)命令。

如果启用详细调试程序输出时，调试器将显示总数的加载和卸载模块时调用该扩展时，调试器将显示有关每个模块即可（包括的每个可用的别名值）的详细的信息*CommandString*执行该模块。

下面的示例演示如何使用 **！ 有关\_每个\_模块**扩展。 下面的命令显示全局调试标志。

```dbgcmd
!for_each_module x ${@#ModuleName}!*Debug*Flag*
!for_each_module x ${@#ModuleName}!g*Debug*
```

以下命令通过使用检查每个已加载模块中的二进制损坏[ **！ chkimg** ](-chkimg.md)扩展：

```dbgcmd
!for_each_module !chkimg @#ModuleName
```

以下命令会搜索每个加载的映像中的模式"MZ"。

```dbgcmd
!for_each_module s-a @#Base @#End "MZ"
```

下面的示例演示如何使用 @\#FileVersion 和 @\#ProductVersion 对于每个模块名称：

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

 

 





