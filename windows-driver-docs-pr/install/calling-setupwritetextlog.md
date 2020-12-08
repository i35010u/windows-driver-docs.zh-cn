---
title: 调用 SetupWriteTextLog
description: 调用 SetupWriteTextLog
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 59397a3eae8de77b7c397e01153e6ce270221a1e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814405"
---
# <a name="calling-setupwritetextlog"></a>调用 SetupWriteTextLog


[**SetupWriteTextLog**](/windows/win32/api/setupapi/nf-setupapi-setupwritetextlog) 将包含有关安装事件的信息的单个条目添加到 [setupapi.log 文本日志](setupapi-text-logs.md)中。

如 [文本日志节正文的格式](format-of-a-text-log-section-body.md)中所述，日志条目的格式由以下字段组成：

```cpp
entry_prefix time_stamp event_category indentation formatted_message
```

若要调用 **SetupWriteTextLog**，应用程序提供以下信息：

-   文本日志中某节的日志标记，该标记是通过调用 [**SetupGetThreadLogToken**](/windows/win32/api/setupapi/nf-setupapi-setupgetthreadlogtoken)或某个系统定义的 [日志令牌](log-tokens.md)获取的。 如果日志令牌与文本日志部分关联，则 **SetupWriteTextLog** 会在该部分写入日志项。 否则， **SetupWriteTextLog** 会将日志条目添加到不包含在文本日志节中的日志部分。 此外， **SetupWriteTextLog** 是否会写入日志条目，以及是否将条目写入到哪个文本日志 **SetupWriteTextLog** ，具体取决于系统定义的日志令牌值。

    有关日志令牌的详细信息，请参阅 [设置和获取线程的日志令牌](setting-and-getting-a-log-token-for-a-thread.md)。

-   为 [文本日志启用事件类别](enabling-event-categories-for-a-text-log.md)中描述的一种事件类别。 如果为文本日志启用了项的事件类别，则 [**SetupWriteTextLog**](/windows/win32/api/setupapi/nf-setupapi-setupwritetextlog) 会将该项添加到文本日志中;否则， **SetupWriteTextLog** 不会将条目写入文本日志。

-   一个标志值，它是系统定义的常量的按位 "或"，用于指定事件级别、缩进深度以及是否包含时间戳。 [设置文本日志的事件级别](setting-the-event-level-for-a-text-log.md)中介绍了事件级别。 如果为文本日志设置的事件级别大于或等于该条目的事件级别，则 **SetupWriteTextLog** 会将日志条目写入文本日志;否则， **SetupWriteTextLog** 不会将日志条目写入文本日志。 通过使用缩进，可以排列经过格式的消息，使节中的信息更易于阅读和理解。 有关详细信息，请参阅 [写入缩进的日志条目](writing-indented-log-entries.md)。

-   一个 **printf** 兼容的格式字符串，用于对消息和格式字符串之后的以逗号分隔的变量列表进行格式设置。

-   以逗号分隔的变量列表，其值由 **printf** 兼容的格式字符串进行格式设置。

有关如何调用 [**SetupWriteTextLog**](/windows/win32/api/setupapi/nf-setupapi-setupwritetextlog) 来记录不是错误或警告事件的信息的示例，请参阅 [编写信息日志条目](writing-an-information-log-entry.md)。

有关如何调用 **SetupWriteTextLog** 来记录有关错误或警告的信息，请参阅 [编写错误或警告日志条目](writing-an-error-or-warning-log-entry.md)。

 

