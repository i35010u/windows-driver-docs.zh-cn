---
title: 命令项格式
description: 命令项格式
keywords:
- 打印机命令 WDK Unidrv，输入格式
- 格式化 WDK 打印机命令
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d73597685f73a77ee0231362d0788bfe65052ea8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797665"
---
# <a name="command-entry-format"></a>命令项格式





若要在 GPD 文件中指定打印机命令项，请使用以下格式：

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>* 命令</strong>： <em>CommandName</em> {<em>CommandAttributes</em>}</p></td>
</tr>
</tbody>
</table>

 

其中， *CommandName* 是预定义的 [命令名称](command-names.md)之一， *CommandAttributes* 是一组 [命令属性](command-attributes.md)。

例如，GPD 文件可能包含 CmdStartPage 命令的以下规范，用于初始化打印页面。

```cpp
*Command: CmdStartPage
{
    *Order: PAGE_SETUP.100
    *Cmd: "<0D>"
}
```

如果对于特定的 *CommandName* 值，只需指定 \* Cmd 属性，就可以使用命令条目格式的缩短版本，如下所示：

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>* 命令</strong>： <em>CommandName</em>： <em>command.commandstring</em></p></td>
</tr>
</tbody>
</table>

 

其中， *command.commandstring* 是表示打印机命令转义序列的文本字符串。 有关指定转义序列的详细信息，请参阅 [命令字符串格式](command-string-format.md)。

例如，GPD 文件可能包含 CmdBoldOn 命令的以下规范，此规范将打开粗体文本：

```cpp
*Command: CmdBoldOn: "<1B>(s3B"
```

 

 




