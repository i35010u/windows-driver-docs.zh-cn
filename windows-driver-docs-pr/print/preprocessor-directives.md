---
title: 预处理器指令
description: 预处理器指令
keywords:
- GPD 文件条目 WDK Unidrv，预处理器指令
- 预处理器指令 WDK GPD 文件
- 分析 GPD 文件部分
- 预处理器符号 WDK GPD 文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 28d76d8d6dd09194b9a398812f267103d600ab4f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807517"
---
# <a name="preprocessor-directives"></a>预处理器指令





GPD 文件可以包含预处理器指令，这些指令可用于控制 GPD 文件中部分的条件分析。 下表描述了可在 GPD 文件中使用的预处理器指令。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>PreprocessorDirective</th>
<th>定义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em><strong>定义</strong>： <em>SymbolName</em></p></td>
<td><p>定义一个符号。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>取消定义 </strong> ： <em>SymbolName</em></p></td>
<td><p>删除以前定义的符号。</p></td>
</tr>
<tr class="odd">
<td><p><em><strong>Ifdef</strong> ： <em>SymbolName</em></p></td>
<td><p>指示 GPD 文件条目块的开头。</p>
<p>如果定义了指定的符号，则 GPD 分析器处理此指令和下一个 *<strong>Ifdef</strong>、*<strong>Elseifdef</strong>、*<strong>Else</strong>或 *<strong>Endif</strong> 指令之间的 GPD 文件项。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>Elseifdef </strong> ： <em>SymbolName</em></p></td>
<td><p>如果定义了指定的符号，且未定义前面的 <em> <strong>Ifdef</strong>或 *<strong>Elseifdef</strong>指令指定的符号，则 GPD 分析器将处理此指令与下一个 *<strong>Ifdef</strong>、*<strong>Elseifdef</strong>、*<strong>Else</strong>或 *<strong>Endif</strong>指令之间的 GPD 文件项。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>否则 </strong> ：</p></td>
<td><p>如果未定义前面的 <em> <strong>Ifdef</strong>或 *<strong>Elseifdef</strong>指令指定的符号，则 GPD 分析器将处理此指令和下一个 *<strong>Ifdef</strong>或 *<strong>Endif</strong>指令之间的 GPD 文件项。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>Endif </strong> ：</p></td>
<td><p>指示 GPD 文件条目块的结束。</p></td>
</tr>
<tr class="odd">
<td><p><em><strong>包括</strong> ： "<em>FileName</em>"</p></td>
<td><p>指定其他 GPD 文件的名称。 请参阅 <a href="using-multiple-gpd-files-in-a-minidriver.md" data-raw-source="[Using Multiple GPD Files in a Minidriver](using-multiple-gpd-files-in-a-minidriver.md)">在微型驱动程序中使用多个 GPD 文件</a>。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>SetPPPrefix </strong> ： <em>PrefixString</em></p></td>
<td><p>更改预先为预处理器指令的前缀字符串。 请参阅 <strong>更改预处理器指令前缀</strong> 部分。</p></td>
</tr>
</tbody>
</table>

 

条件预处理器指令可以嵌套。 在每个嵌套级别，使用条件预处理器指令的顺序如下所示：

\***Ifdef**： *Symbol1* GPD file 部分

\***Elseifdef**： *Symbol2* GPD file 部分

\***Elseifdef**： *Symbol3* GPD file 部分

\***Elseifdef**： *Symbol4* GPD file 部分

...

\***Else**： GPD 文件部分

\**_Endif_*：

对于所使用的每个 \* *_Ifdef_* 指令， \* *_Endif_* 是必需的。 \* *_Elseifdef_* 和 \* *_Else_* 指令是可选的。 每个 GPD 文件部分都可以包含 GPD 文件项，还可以包含一组嵌套的条件预处理器指令。

使用 Define 定义的所有符号在 \* *_Define_* 使用 undefined 显式定义之前始终定义 \* *_Undefine_*。

\* *_Include_* 指令允许您指定其他 GPD 文件的名称。 有关详细信息，请参阅 [在微型驱动程序中使用多个 GPD 文件](using-multiple-gpd-files-in-a-minidriver.md)。

请注意， \* IGNOREBLOCK GPD 项不影响预处理器指令，因为预处理器在 GPD 分析器之前执行。

### <a name="changing-the-preprocessor-directive-prefix"></a><a href="" id="ddk-changing-the-preprocessor-directive-prefix-gg"></a>更改预处理器指令前缀

使用 \* **SetPPPrefix** 指令，可以更改与预处理器指令一起使用的前缀。 也就是说，您可以使用此指令替换 \* 前面带有其他字符或字符串的预处理器指令的星号 () 字符。

例如，如果 GPD 文件包含以下指令：

```cpp
*SetPPPrefix: #SpecialPrefix#
```

然后，预处理器将停止搜索以 _ 开头的预处理器指令， **\* *而是查找以 _* \# SpecialPrefix \# 开头的指令**。 以下顺序将预处理器前缀暂时更改为 **\# SpecialPrefix \#**，然后将其还原为 * *\** _。

```cpp
_SetPPPrefix: #SpecialPrefix#
#SpecialPrefix#Ifdef: WINNT_50
#SpecialPrefix#Include: "ExtraGPD.gpd"
#SpecialPrefix#Endif:
#SpecialPrefix#SetPPPrefix: *
```

此功能的主要用途是允许为将来的操作系统版本编写的 GPD 文件与 Windows 2000 兼容。 例如，假设操作系统的未来版本的 GPD 文件可以包含与 Windows 2000 支持的星号前缀预处理器指令冲突的 GPD 文件条目。 通过更改前缀，为将来的操作系统版本编写的 GPD 文件也可以与 Windows 2000 一起使用。 可以按如下所示构造一个示例：

```cpp
*Ifdef: WINNT_70
    *SetPPPrefix: #SpecialPrefix#
    *% Do special, OS-specific processing of
    *% GPD file entries that might conflict with
    *% asterisk-prefixed preprocessor directives.
    #SpecialPrefix#SetPPPrefix: *
*Endif:
```

请注意，此方法仅更改预处理器查找的前缀。 分析器识别的关键字必须始终以星号开头。

### <a name="predefined-preprocessor-symbols"></a><a href="" id="ddk-predefined-preprocessor-symbols-gg"></a>预定义的预处理器符号

Microsoft 定义以下预处理器符号。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>符号</th>
<th>定义位置</th>
<th>定义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WINNT_51</p></td>
<td><p>适用于 Windows XP 的 GPD 预处理器</p></td>
<td><p>环境为 Windows XP。</p></td>
</tr>
<tr class="even">
<td><p>WINNT_50</p></td>
<td><p>适用于 Windows XP 和 Windows 2000 的 GPD 预处理器</p></td>
<td><p>环境为 Windows 2000。</p></td>
</tr>
<tr class="odd">
<td><p>WINNT_40</p></td>
<td><p>适用于 Windows XP、Windows 2000 和 Windows NT 4.0 的 GPD 预处理器</p></td>
<td><p>环境为 Windows NT 4.0。</p></td>
</tr>
<tr class="even">
<td><p>PARSER_VER_1 0</p></td>
<td><p>适用于 Windows NT 4.0、Windows 2000 和 Windows XP 的 GPD 预处理器</p></td>
<td><p>GPD 分析器版本1。0</p></td>
</tr>
</tbody>
</table>

 

WINNT \_ 40、winnt \_ 50 和 winnt \_ 51 符号可用于创建与 windows NT 4.0、Windows 2000 和 windows XP 兼容的 GPD 文件。 例如，如果 Windows XP 支持 Windows 2000 不支持的打印机功能，则可在 GPD 文件的节中指定该功能，该文件将由 \* **Ifdef**： WINNT \_ 51 和 \* *_Endif_* 指令进行限定。

 

 




