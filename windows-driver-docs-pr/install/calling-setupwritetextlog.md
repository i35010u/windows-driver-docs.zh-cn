---
title: 调用 SetupWriteTextLog
description: 调用 SetupWriteTextLog
ms.assetid: a07118ae-bef6-4d01-94d9-98587cbff863
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f773a992c586959a5c2e976132b8e1b03e0665f3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385282"
---
# <a name="calling-setupwritetextlog"></a>调用 SetupWriteTextLog


[**SetupWriteTextLog** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupwritetextlog)添加到安装事件的相关信息与单个条目[SetupAPI 文本日志](setupapi-text-logs.md)。

如中所述[格式的文本日志部分正文](format-of-a-text-log-section-body.md)，日志条目的格式包含以下字段：

```cpp
entry_prefix time_stamp event_category indentation formatted_message
```

若要调用**SetupWriteTextLog**，应用程序提供以下信息：

-   通过调用获取了文本日志中的某个部分的日志标记[ **SetupGetThreadLogToken**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupgetthreadlogtoken)，或其中一个系统定义[登录令牌](log-tokens.md)。 如果日志标记为与文本日志部分中，相关联**SetupWriteTextLog**在该部分中写入该日志条目。 否则为**SetupWriteTextLog**将日志条目添加到不包含文本日志部分中的日志的一部分。 此外，无论**SetupWriteTextLog**写入日志项，以及哪些文本日志**SetupWriteTextLog**写入条目，取决于系统定义的日志标记值。

    有关日志令牌的详细信息，请参阅[设置和获取日志标记线程](setting-and-getting-a-log-token-for-a-thread.md)。

-   一个事件类别中所述[启用文本日志的事件类别](enabling-event-categories-for-a-text-log.md)。 如果文本日志中，为启用了该条目的事件类别[ **SetupWriteTextLog** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupwritetextlog)将项添加到文本日志; 否则为**SetupWriteTextLog**不会写入文本日志条目。

-   一个标志值，它是指定的事件级别、 缩进深度，以及是否包括时间戳的系统定义的常量的按位 OR。 事件级别中所述[事件级别设置为文本日志](setting-the-event-level-for-a-text-log.md)。 如果事件级别设置为文本日志将是大于或等于该注册表项，事件的事件级别**SetupWriteTextLog**将日志条目写入到文本日志中; 否则为**SetupWriteTextLog**不会写入日志文本日志条目。 通过使用缩进，可以排列格式化的消息来使一个部分中的信息更轻松地阅读和理解。 有关详细信息，请参阅[写入缩进日志条目](writing-indented-log-entries.md)。

-   一个**printf**-兼容的格式字符串设置格式的消息和格式字符串之后的逗号分隔的变量列表。

-   逗号分隔的变量，其值设置格式的列表**printf**-兼容的格式字符串。

有关如何调用示例[ **SetupWriteTextLog** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupwritetextlog)若要记录不是错误或警告的事件有关的信息，请参阅[写入信息日志条目](writing-an-information-log-entry.md)。

有关如何调用示例**SetupWriteTextLog**若要记录有关错误或警告的信息，请参阅[编写错误或警告日志条目](writing-an-error-or-warning-log-entry.md)。

 

 





