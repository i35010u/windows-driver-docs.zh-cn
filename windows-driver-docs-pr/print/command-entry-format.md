---
title: 命令条目格式
description: 命令条目格式
ms.assetid: f2b14c12-3c34-45b2-9ead-8cd57d657e9e
keywords:
- 打印机命令 WDK Unidrv，条目格式
- 格式 WDK 打印机命令
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: da6a4734f4555ecfe543cdcfc11b01891806f9e2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556016"
---
# <a name="command-entry-format"></a>命令条目格式





若要 GPD 文件中指定的打印机命令项，请使用以下格式：

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>* 命令</strong>:<em>CommandName</em> {<em>CommandAttributes</em>}</p></td>
</tr>
</tbody>
</table>

 

其中*CommandName*是预定义的[命令名](command-names.md)，并*CommandAttributes*是一套[命令属性](command-attributes.md)。

例如，GPD 文件可能包含以下 CmdStartPage 命令，初始化要打印的页的规范。

```cpp
*Command: CmdStartPage
{
    *Order: PAGE_SETUP.100
    *Cmd: "<0D>"
}
```

当对于特定*CommandName*值，您只需指定\*Cmd 属性，可以使用命令条目格式，按如下所示的缩写的形式：

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>* 命令</strong>:<em>CommandName</em>:<em>CommandString</em></p></td>
</tr>
</tbody>
</table>

 

其中*CommandString*是表示打印机命令转义序列的文本字符串。 有关指定转义序列的详细信息，请参阅[命令字符串格式](command-string-format.md)。

例如，GPD 文件可能包含 CmdBoldOn 命令，可将粗体文本上的以下规范：

```cpp
*Command: CmdBoldOn: "<1B>(s3B"
```

 

 




