---
title: 文本字符串
description: 文本字符串
keywords:
- GPD 文件条目 WDK Unidrv，文本字符串
- 文本字符串 WDK GPD 文件
- 字符串 WDK GPD 文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eb84263683e04f36638a1fe393d177162dd0c3e4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806703"
---
# <a name="text-strings"></a>文本字符串





文本字符串是使用引号分隔的文本字符字符串。 [Unidrv 微型驱动程序](unidrv-minidrivers.md)使用的字符串可以放置在以下两个位置之一：

-   它们可以放在资源文件中。 需要本地化的字符串（例如用户界面文本）应放在资源文件中，如在 [微型驱动程序中使用资源 dll](using-resource-dlls-in-a-minidriver.md)中所述。

-   它们可以包括在 GPD 文件中。 表示构成打印机命令的转义序列的字符串通常包含在 GPD 文件中，因为这些字符串不需要本地化。

字符串必须遵守以下规则：

-   字符串必须用引号分隔 ( "..." ) 。

-   可以通过将十六进制数字用尖括号分隔 (&lt; ... &gt;) ，如 &lt; 03 &gt; 或 &lt; 1b， &gt; 来将十六进制字节值放入字符串。 在一组尖括号中，每对数字被解释为另一个十六进制字节值。 因此， &lt; 3 &gt; &lt; 1B &gt; 、 &lt; 03 1b &gt; 和 &lt; 031B &gt; 都是等效的。

-   百分号 (% ) 用作转义字符。 若要在字符串中包含引号或左尖括号 ( " &lt;) ，请在字符串前面加上百分号。 若要指定以百分号结尾的字符串，必须为% 指定十六进制值，如 "25" 中所示 &lt; &gt; 。

    此外，若要在表示 [打印机命令](printer-commands.md)的文本字符串中包含百分号，则必须在其前面加上百分号。 若要指定以百分号结尾的打印机命令，必须指定两个十六进制百分比值，如下所示：

    "command-string &lt; 25 25 &gt; "

示例字符串是用于选择 Canon BJC-600 打印机的 letter 大小纸张的命令。 此命令是字节序列 1B 28 67 03 00 6E 01 72，可以指定为：

" &lt; 1b &gt; (g &lt; 03 00 &gt; n &lt; 01 &gt; r"

字符串中包含的每个 ASCII 字符都转换为它的单字节十六进制等效项。

-   GPD 文件中包含的字符串必须遵守以下附加规则：

    若要将字符串扩展到单个行以外，请在第一个行的前面加上 [行继续](line-continuation.md) 符 (+) ，并用引号分隔每一行上的文本。

-   一个字符串值可以包含多个文本字符串。 例如，以下两个 GPD 项是等效的：
    ```cpp
    *Name: "abc""def" *% Comment
    +      "gh"    "ijk"

    *Name: "abcdefghijk"
    ```

有关与资源文件中定义的字符串有关的其他规则，请参阅 Microsoft Windows SDK 文档中的 STRINGTABLE 语句说明。

有关指定打印机命令转义序列的详细信息，请参阅 [命令字符串格式](command-string-format.md)。

 

 




