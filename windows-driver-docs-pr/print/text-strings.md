---
title: 文本字符串
description: 文本字符串
ms.assetid: 773c977b-aac4-4c7c-8bab-aa2c69b2a89a
keywords:
- GPD 文件条目 WDK Unidrv，文本字符串
- 文本字符串 WDK GPD 文件
- 字符串 WDK GPD 文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f32e1065a3e4562bbb7f561709e913c0df3a3cc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543557"
---
# <a name="text-strings"></a>文本字符串





文本字符串是文本字符、 引号分隔的字符串。 使用的字符串[Unidrv 微型驱动程序](unidrv-minidrivers.md)可以放入两个位置之一：

-   可以将它们放在资源文件中。 需要本地化，例如用户界面文本的字符串应放置在资源文件，如中所述[微型驱动程序中使用资源 Dll](using-resource-dlls-in-a-minidriver.md)。

-   它们可以包含在 GPD 文件中。 表示构成了打印机命令的转义序列的字符串是通常包含在 GPD 文件，因为这些字符串不需要本地化。

字符串必须遵循下列规则：

-   字符串必须用引号 （"..."） 分隔。

-   十六进制字节的值可以在字符串中放置尖括号由分隔的十六进制数字 (&lt;...&gt;)，如&lt;03&gt;或&lt;1B&gt;。 在尖括号内一组，每个一组数字被解释为另一个十六进制字节值。 因此&lt;03&gt;&lt;1B&gt;， &lt;03 1B&gt;，以及&lt;031B&gt;都是等效的。

-   百分号 （%）用作转义符。 若要包含引号或左的尖括号 ("， &lt;) 在字符串内，它在前面加上百分号。 若要指定结尾百分比符号的字符串，必须指定的十六进制值为 %，如"&lt;25&gt;"。

    此外，若要包括一个百分号在文本中的符号表示的字符串[打印机命令](printer-commands.md)，您必须前面加上另一个的百分比符号。 若要指定结尾百分比符号的打印机命令，必须指定两个十六进制 %值如

    "命令字符串&lt;25 25&gt;"

字符串的示例是选择信纸尺寸的纸张 Canon BJC-600 打印机的命令。 此命令中，这是字节序列 1B 28 67 03 00 6E 01 72，可以指定为：

"&lt;1B&gt;(g&lt;03 00&gt;n&lt;01&gt;r"

包含在字符串中的每个 ASCII 字符转换为单字节十六进制的等值。

-   GPD 文件中包含的字符串必须遵循下列附加规则：

    若要扩展超出单个行的字符串，位于每个行后的第一个[行继续符](line-continuation.md)字符 （+），并分隔在每个行中使用引号引起来的文本。

-   一个字符串值可以包含多个文本字符串。 例如，以下两个 GPD 条目是等效的：
    ```cpp
    *Name: "abc""def" *% Comment
    +      "gh"    "ijk"

    *Name: "abcdefghijk"
    ```

有关与资源文件中定义的字符串相关的其他规则，请参阅 Microsoft Windows SDK 文档中的 STRINGTABLE 语句说明。

有关指定打印机命令转义序列的详细信息，请参阅[命令字符串格式](command-string-format.md)。

 

 




