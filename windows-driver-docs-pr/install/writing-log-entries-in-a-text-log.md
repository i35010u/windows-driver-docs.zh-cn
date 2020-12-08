---
title: 在文本日志中写入日志条目
description: 在文本日志中写入日志条目
keywords:
- 文本日志 WDK Setupapi.log，写入条目
- 节 WDK Setupapi.log 日志记录
- 文本日志 WDK Setupapi.log，章节
- 写入文本日志条目
- Setupapi.log 日志记录 WDK Windows Vista，文本日志部分
- Setupapi.log 日志记录 WDK Windows Vista，编写文本日志条目
- SetupWriteTextLog
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7bbfbdc4e887be7c5d4e8da3c734bc33968315c8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840920"
---
# <a name="writing-log-entries-in-a-text-log"></a>在文本日志中写入日志条目


应用程序执行以下操作之一，在 [setupapi.log 文本日志](setupapi-text-logs.md)中写入日志条目：

-   [调用 SetupWriteTextLog](calling-setupwritetextlog.md) 来写入包含有关安装事件的信息的单个文本日志项。

-   [调用 SetupWriteTextLogError](calling-setupwritetextlogerror.md) ，将有关特定于 setupapi.log 的错误或 Win32 错误的信息写入文本日志。 **SetupWriteTextLogError** 将两个连续条目写入到文本日志中：第一个条目包含的信息的格式与 **SetupWriteTextLog** 编写的格式相同，第二个条目记录对应的错误代码和对错误的用户友好说明。

-   [调用 SetupWriteTextLogInfLine](calling-setupwritetextloginfline.md) 来写入包含指定 INF 文件行的文本的单个文本日志项。

如 [文本日志节正文的格式](format-of-a-text-log-section-body.md)中所述，setupapi.log 日志记录函数以以下格式写入条目：

```cpp
entry_prefix time_stamp event_category indentation formatted_message
```

各种 Setupapi.log 日志记录功能写入文本日志的条目之间的主要区别在于具体的信息内容和 *格式化消息* 字段的格式。

有关如何设置 *缩* 进字段以缩进 *格式化消息* 字段的信息，请参阅 [写入缩进的日志条目](writing-indented-log-entries.md)。

 

 





