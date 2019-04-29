---
title: 预处理器指令
description: 预处理器指令
ms.assetid: 5731b159-c6f9-47a8-8eaa-a1b0b6c12132
keywords:
- GPD 文件条目 WDK Unidrv，预处理器指令
- 预处理器指令 WDK GPD 文件
- 分析 GPD 文件部分
- 预处理器符号 WDK GPD 文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d4d8a855c0cfc79cfd2ce46480ce8ff6c2fcaf01
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389487"
---
# <a name="preprocessor-directives"></a>预处理器指令





GPD 文件可以包含预处理器指令，可用于控制 GPD 文件中节的条件性分析。 下表介绍可以 GPD 文件中使用的预处理器指令。

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
<td><p><em><strong>定义</strong>:<em>SymbolName</em></p></td>
<td><p>定义的符号。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>取消定义</strong>:<em>SymbolName</em></p></td>
<td><p>删除以前定义的符号。</p></td>
</tr>
<tr class="odd">
<td><p><em><strong>Ifdef</strong> :<em>SymbolName</em></p></td>
<td><p>指示 GPD 文件条目的块的开头。</p>
<p>如果定义指定的符号，则 GPD 文件之间此指令和下一项 *<strong>Ifdef</strong>，*<strong>Elseifdef</strong>，*<strong>Else</strong>，或 *<strong>Endif</strong>GPD 分析器处理指令。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>Elseifdef</strong> :<em>SymbolName</em></p></td>
<td><p>如果定义了指定的符号，并且先前指定的符号<em> <strong>Ifdef</strong>或 *<strong>Elseifdef</strong>指令是不确定，此指令和下一步之间的 GPD 文件条目 *<strong>Ifdef</strong>，*<strong>Elseifdef</strong>，*<strong>Else</strong>，或 *<strong>Endif</strong> GPD 分析器处理指令。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>其他</strong>:</p></td>
<td><p>如果先前指定的符号<em> <strong>Ifdef</strong>或 *<strong>Elseifdef</strong>指令是不确定，此指令和下一步之间的 GPD 文件条目 *<strong>Ifdef</strong>或 *<strong>Endif</strong> GPD 分析器处理指令。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>Endif</strong> :</p></td>
<td><p>指示 GPD 文件条目的块的末尾。</p></td>
</tr>
<tr class="odd">
<td><p><em><strong>包括</strong>:"<em>FileName</em>"</p></td>
<td><p>指定其他 GPD 文件的名称。 请参阅<a href="using-multiple-gpd-files-in-a-minidriver.md" data-raw-source="[Using Multiple GPD Files in a Minidriver](using-multiple-gpd-files-in-a-minidriver.md)">微型驱动程序中使用多个 GPD 文件</a>。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>SetPPPrefix</strong> :<em>PrefixString</em></p></td>
<td><p>更改预处理器指令前预置的前缀字符串。 请参阅<strong>更改的预处理器指令前缀</strong>部分。</p></td>
</tr>
</tbody>
</table>

 

可以嵌套条件预处理器指令。 在每个嵌套级别，使用条件预处理器指令的顺序如下所示：

\***Ifdef**:*Symbol1* GPD 文件部分

\***Elseifdef**:*Symbol2* GPD 文件部分

\***Elseifdef**:*Symbol3* GPD 文件部分

\***Elseifdef**:*Symbol4* GPD 文件部分

...

\***其他**:GPD 文件部分

\***Endif**:

每个\* **Ifdef**使用，指令\* **Endif**是必需的。 \* **Elseifdef**并\* **Else**指令为可选。 每个 GPD 文件部分可以包含 GPD 文件条目和嵌套的条件预处理器指令序列 （可选）。

使用定义的所有符号\***定义**直到显式未定义的使用保持已定义\***未定义**。

\* **Include**指令允许您指定其他 GPD 文件的名称。 有关详细信息，请参阅[微型驱动程序中使用多个 GPD 文件](using-multiple-gpd-files-in-a-minidriver.md)。

请注意， \*IgnoreBlock GPD 条目不会影响预处理器指令，因为之前 GPD 分析器执行预处理器。

### <a href="" id="ddk-changing-the-preprocessor-directive-prefix-gg"></a>更改预处理器指令前缀

\* **SetPPPrefix**指令使你能够更改与预处理器指令一起使用的前缀。 也就是说，可以使用此指令替换星号 (\*) 前面添加的预处理器指令与另一个字符或字符串的字符。

例如，如果 GPD 文件包含以下指令：

```cpp
*SetPPPrefix: #SpecialPrefix#
```

然后预处理器就停止搜索以开头的预处理器指令**\\***，并改为查找指令开头**\#SpecialPrefix\#**. 以下序列暂时更改的预处理器前缀 **\#SpecialPrefix\#**，然后还原到 * *\\* * *。

```cpp
*SetPPPrefix: #SpecialPrefix#
#SpecialPrefix#Ifdef: WINNT_50
#SpecialPrefix#Include: "ExtraGPD.gpd"
#SpecialPrefix#Endif:
#SpecialPrefix#SetPPPrefix: *
```

此功能的主要用途是允许 GPD 文件才能与 Windows 2000 兼容的将来的操作系统版本编写的。 例如，假设的未来版本的操作系统的 GPD 文件可以包括与支持的 Windows 2000 的星号前缀的预处理器指令发生冲突的 GPD 文件条目。 通过更改前缀，写入以供将来的操作系统版本 GPD 文件还可以与 Windows 2000 一起使用。 一个示例可能按以下方式构造：

```cpp
*Ifdef: WINNT_70
    *SetPPPrefix: #SpecialPrefix#
    *% Do special, OS-specific processing of
    *% GPD file entries that might conflict with
    *% asterisk-prefixed preprocessor directives.
    #SpecialPrefix#SetPPPrefix: *
*Endif:
```

请注意，此方法只会更改预处理器会查找的前缀。 分析器可识别关键字后面必须跟一个星号。

### <a href="" id="ddk-predefined-preprocessor-symbols-gg"></a>预定义的预处理器符号

Microsoft 定义了以下预处理器符号。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>符号</th>
<th>在此定义</th>
<th>定义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WINNT_51</p></td>
<td><p>GPD 适用于 Windows XP 预处理器</p></td>
<td><p>环境是 Windows XP。</p></td>
</tr>
<tr class="even">
<td><p>WINNT_50</p></td>
<td><p>GPD 适用于 Windows XP 和 Windows 2000 预处理器</p></td>
<td><p>环境是 Windows 2000。</p></td>
</tr>
<tr class="odd">
<td><p>WINNT_40</p></td>
<td><p>适用于 Windows XP、 Windows 2000 和 Windows NT 4.0 GPD 预处理器</p></td>
<td><p>环境是 Windows NT 4.0。</p></td>
</tr>
<tr class="even">
<td><p>PARSER_VER_1.0</p></td>
<td><p>有关 Windows NT 4.0、 Windows 2000 和 Windows XP GPD 预处理器</p></td>
<td><p>GPD 分析器版本 1.0</p></td>
</tr>
</tbody>
</table>

 

WINNT\_40，WINNT\_50 和 WINNT\_51 符号可用于创建使用 Windows NT 4.0、 Windows 2000 和 Windows XP 兼容的 GPD 文件。 如果，例如，Windows XP 支持 Windows 2000 不支持的打印机功能，则该功能可以指定在受某 GPD 文件一部分\* **Ifdef**:WINNT\_51 和\* **Endif**指令。

 

 




