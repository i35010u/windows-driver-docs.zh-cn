---
title: 在文本日志中写入日志条目
description: 在文本日志中写入日志条目
ms.assetid: e969f8dd-ad19-42d5-8218-3df0633cc304
keywords:
- 文本日志 WDK SetupAPI，写入项
- 部分 WDK SetupAPI 日志记录
- 文本日志 WDK SetupAPI，部分
- 编写文本日志条目
- SetupAPI 日志记录 WDK Windows Vista 中，文本日志部分
- SetupAPI 日志记录 WDK Windows Vista、 编写文本日志条目
- SetupWriteTextLog
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: faef4ed68c07f2bbf09f3564bc551cd868378764
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339144"
---
# <a name="writing-log-entries-in-a-text-log"></a>在文本日志中写入日志条目


应用程序执行的一种操作将日志项写入[SetupAPI 文本日志](setupapi-text-logs.md):

-   [调用 SetupWriteTextLog](calling-setupwritetextlog.md)写入单个文本日志项包含有关安装事件的信息。

-   [调用 SetupWriteTextLogError](calling-setupwritetextlogerror.md)有关特定于安装程序 Api 的错误或 Win32 错误的信息写入到文本日志。 **SetupWriteTextLogError**将两个连续的条目写入到文本日志： 第一个条目包含相同的信息与写入的相同的格式**SetupWriteTextLog**和第二个条目记录对应错误代码和错误的用户友好说明。

-   [调用 SetupWriteTextLogInfLine](calling-setupwritetextloginfline.md)写入单个文本日志项包含指定的 INF 文件行的文本。

如中所述[格式的文本日志部分正文](format-of-a-text-log-section-body.md)、 SetupAPI 记录函数写入条目采用以下格式：

```cpp
entry_prefix time_stamp event_category indentation formatted_message
```

各种 SetupAPI 日志记录功能将写入到文本日志条目之间的主要区别是和中的特定信息内容的格式*格式化消息*字段。

有关如何设置的信息*缩进*字段来缩进*格式化消息*字段中，请参阅[写入缩进日志条目](writing-indented-log-entries.md)。

 

 





