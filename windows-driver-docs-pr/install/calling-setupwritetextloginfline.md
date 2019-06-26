---
title: 调用 SetupWriteTextLogInfLine
description: 调用 SetupWriteTextLogInfLine
ms.assetid: 7b7a08bf-b97a-4dfe-8695-dc947481ad2b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b3be10d93460f9a86e720920a7a36a01b0bb492
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385280"
---
# <a name="calling-setupwritetextloginfline"></a>调用 SetupWriteTextLogInfLine


应用程序可以调用[ **SetupWriteTextLogInfLine** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupwritetextloginfline)将日志项写入[SetupAPI 文本日志](setupapi-text-logs.md)，包含指定的 INF 文件行的文本。

若要调用**SetupWriteTextLogInfLine**，应用程序提供以下信息：

-   通过调用获取了文本日志中的某个部分的日志标记[ **SetupGetThreadLogToken** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupgetthreadlogtoken)或其中一个系统定义[登录令牌](log-tokens.md)。 如果日志标记为与文本日志部分中，相关联**SetupWriteTextLogInfLine**在该部分中写入该日志条目。 否则为**SetupWriteTextLogInfLine**将日志条目添加到不包含文本日志部分中的日志的一部分。

    此外，无论**SetupWriteTextLogInfLine**写入日志项，以及哪些文本日志**SetupWriteTextLogInfLine**写入条目，取决于系统定义的日志标记值。

    有关日志令牌的详细信息，请参阅[设置和获取日志标记线程](setting-and-getting-a-log-token-for-a-thread.md)。

-   一个标志值，它是指定的事件级别、 缩进深度，以及是否包括时间戳的系统定义的常量的按位 OR。 事件级别中所述[事件级别设置为文本日志](setting-the-event-level-for-a-text-log.md)。

    如果事件级别设置为文本日志将是大于或等于该注册表项，事件的事件级别[ **SetupWriteTextLogInfLine** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupwritetextloginfline)文本日志中写入日志项。 否则为**SetupWriteTextLogInfLine**不会写入日志项的文本日志中。 通过使用缩进，可以排列格式化的消息来使一个部分中的信息更轻松地阅读和理解。

    有关详细信息，请参阅[写入缩进日志条目](writing-indented-log-entries.md)。

-   包含的 INF 文件行的 INF 文件句柄。

-   INF 文件行上下文。

**SetupWriteTextLogInfLine**采用以下格式写入日志项：

*entry_prefix time_stamp* **inf:** <em>indentation inf-line-text</em> **(** <em>inf-file-name</em> **line** <em>line-number</em> **)**

其中：

-   *Entry_prefix*，*时间戳*，并*缩进*字段将与中所述的相同[格式的文本日志部分正文](format-of-a-text-log-section-body.md).

-   **Inf:** 字段指定 TXTLOG_INF 事件类别。 事件类别中所述[启用文本日志的事件类别](enabling-event-categories-for-a-text-log.md)。

-   *Inf 行文本*字段中包含指定的 INF 文件行的文本。

-   *Inf 文件名*字段包含的 INF 文件包含指定的 INF 文件行的名称。

-   **行**字段指示以下内容是 INF 文件中的行号。

-   *行号*字段包含的 INF 文件中的指定行的行号。

下面的示例演示应用程序可能通常文本日志中记录 INF 行的文本的方式。 在此示例中的 INF 行是 INF **AddReg**行。 应用程序调用[ **SetupWriteTextLogInfLine**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupwritetextloginfline)，提供以下输入的参数值：

-   *LogToken*设置为返回的日志令牌[ **SetupGetThreadLogToken** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupgetthreadlogtoken)或系统定义[日志令牌](log-tokens.md)。

-   *LogFlags*设置为 TXTLOG_DETAILS。 此示例不包括时间戳或更改缩进深度。 在示例中，缩进深度是五个等宽字体的文本空间。

-   *InfHandle*设置为 INF 文件的句柄*hidserv.inf。* 通过调用获取此句柄**SetupOpenInfFile**函数，Platform SDK 中所述。

-   *上下文*设置为包含文本的 INF 文件行的 INF 文件上下文"AddReg = HidServ_AddService_AddReg。" 在行的 INF 文件上下文获取通过调用**SetupFind*Xxx*行**Platform SDK 中记录的函数。

值*LogToken*并*LogFlags*影响的操作[ **SetupWriteTextLogInfLine** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupwritetextloginfline)中所述相同的方式有关[ **SetupWriteTextLog**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupwritetextlog)。 此外， **SetupWriteTextLogInfLine**使用事件目录 TXTLOG_INF。

对于此示例中，以下显示日志项类型的**SetupWriteTextLogInfLine**会写入到文本日志：

```cpp
   inf:      AddReg=HidServ_AddService_AddReg  (hidserv.inf line 98)
```

 

 





