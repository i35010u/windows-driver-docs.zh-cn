---
title: 如何跟踪消息前缀中包含的源行号
description: 如何跟踪消息前缀中包含的源行号
ms.assetid: 07fbdd27-59a9-4fe1-8662-6c2489efdb7f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9bf5bde84c25e0936ad7ccdd4a47eb8a2d564f65
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329881"
---
# <a name="how-to-include-the-source-line-number-in-the-trace-message-prefix"></a>如何在跟踪消息前缀中包含的源行号

WPP 自动记录有关每条跟踪消息，其中的许多默认情况下不显示数据。 此数据包括函数名称、 文件名、 源行号、 组件名称、 子组件名称和跟踪消息的跟踪级别。

若要显示此信息[跟踪消息前缀](trace-message-prefix.md)的优先于每条跟踪消息时，将预定义的前缀变量添加到 %跟踪\_格式\_前缀 %环境变量。 [Tracefmt](tracefmt.md) ，其他跟踪使用者使用 %跟踪\_格式\_格式化跟踪消息时的前缀 %。

例如，若要添加到跟踪消息前缀的组件名称、 函数名称、 文件名和行号，添加以下变量的值 %跟踪\_格式\_前缀 %:

|变量|描述|
|----|----|
|**%!COMPNAME!**|添加组件名称。|
|**%!FUNC!**|添加函数名称。|
|**%2**|添加源代码文件和跟踪语句的行号的名称。|

**%2**变量返回以下字符串：

```command
filename_NNN
```

其中圆点 (**。**) 在文件名称将替换为下划线 (**\_**) 和*NNN*是行号。

以下示例 SET 语句将 **%！COMPNAME**， **%！FUNC ！** 并 **%2** %跟踪的默认值的变量\_格式\_前缀 %。 **！ S ！** 子参数指定的值 **%2**格式化为字符串。 已添加的变量显示为粗体文本显示。

```command
set TRACE\_FORMAT\_PREFIX="\[%9!d!\]%8!04X!.%3!04X!::%4!s! \[%1!s!\](**%!COMPNAME!**:**%!FUNC!**:**%2**!s!)"
```

得到的前缀采用以下格式。 在括号中显示新元素。

\[*CPUNumber*\]*ProcessID*.*ThreadID*::*SystemTime* \[*MessageGUIDFriendlyName*\](*ComponentName*:*FunctionName*:*Filename*\_*LineNumber*)

有关详细示例，请参阅[示例 7:自定义跟踪消息前缀](example-7--customizing-the-trace-message-prefix.md)。 可以出现在跟踪消息前缀的所有预定义变量的列表，请参阅[跟踪消息前缀](trace-message-prefix.md)。
