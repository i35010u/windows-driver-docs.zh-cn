---
title: 如何实现在跟踪消息前缀中包含源行号
description: 如何实现在跟踪消息前缀中包含源行号
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2514a8bab34c4e5db88ccd17b37aae498be32096
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839135"
---
# <a name="how-to-include-the-source-line-number-in-the-trace-message-prefix"></a>如何在跟踪消息前缀中包含源行号

WPP 自动记录有关每个跟踪消息的数据，默认情况下不会显示其中的大多数跟踪消息。 此数据包括函数名、文件名、源行号、组件名称、子组件名称和跟踪消息的跟踪级别。

若要在每个跟踪消息之前的 [跟踪消息前缀](trace-message-prefix.md) 中显示此信息，请将预定义的前缀变量添加到% 跟踪 \_ 格式 \_ 前缀% 环境变量中。 [Tracefmt](tracefmt.md) 和其他跟踪使用者在对 \_ \_ 跟踪消息进行格式设置时使用% trace 格式前缀%。

例如，若要将组件名、函数名、文件名和行号添加到跟踪消息前缀，请将以下变量添加到% 跟踪 \_ 格式 \_ 前缀%：

|变量|描述|
|----|----|
|**%!COMPNAME!**|添加组件名称。|
|**%!求!**|添加函数名称。|
|**%2**|添加源文件的名称和跟踪语句的行号。|

**%2** 变量返回以下字符串：

```command
filename_NNN
```

其中，文件名中的 **点)  (** 替换为下划线 (**\_**) ， *NNN* 为行号。

下面的示例 SET 语句将 **%！COMPNAME**， **%！FUNC！** % **2** 个变量的默认值为% 跟踪 \_ 格式 \_ 前缀%。 **！ S！** 子参数指定将 **%2** 的值设置为字符串格式。 添加的变量显示为粗体文本。

```command
set TRACE\_FORMAT\_PREFIX="\[%9!d!\]%8!04X!.%3!04X!::%4!s! \[%1!s!\](**%!COMPNAME!**:**%!FUNC!**:**%2**!s!)"
```

生成的前缀采用以下格式。 新元素显示在括号中。

\[*CPUNumber* \]*ProcessID*。*ThreadID*：：*SystemTime* \[ *MessageGUIDFriendlyName* \] (*ComponentName*：*FunctionName*：*Filename* \_ *LineNumber*) 

有关详细示例，请参阅 [示例7：自定义跟踪消息前缀](example-7--customizing-the-trace-message-prefix.md)。 有关可出现在跟踪消息前缀中的所有预定义变量的列表，请参阅 [跟踪消息前缀](trace-message-prefix.md)。
