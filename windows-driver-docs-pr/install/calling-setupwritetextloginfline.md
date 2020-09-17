---
title: 调用 SetupWriteTextLogInfLine
description: 调用 SetupWriteTextLogInfLine
ms.assetid: 7b7a08bf-b97a-4dfe-8695-dc947481ad2b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e68c8a26ba28a65981b06ca22465705eda63c8d
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90714718"
---
# <a name="calling-setupwritetextloginfline"></a>调用 SetupWriteTextLogInfLine


应用程序可以调用 [**SetupWriteTextLogInfLine**](/windows/win32/api/setupapi/nf-setupapi-setupwritetextloginfline) 来写入 [setupapi.log 文本日志](setupapi-text-logs.md) 中的日志条目，该日志包含指定的 INF 文件行的文本。

若要调用 **SetupWriteTextLogInfLine**，应用程序提供以下信息：

-   文本日志中某个部分的日志标记，该标记是通过调用 [**SetupGetThreadLogToken**](/windows/win32/api/setupapi/nf-setupapi-setupgetthreadlogtoken) 或某个系统定义的 [日志令牌](log-tokens.md)获取的。 如果日志令牌与文本日志部分关联，则 **SetupWriteTextLogInfLine** 会在该部分写入日志项。 否则， **SetupWriteTextLogInfLine** 会将日志条目添加到不包含在文本日志节中的日志部分。

    此外， **SetupWriteTextLogInfLine** 是否会写入日志条目，以及是否将条目写入到哪个文本日志 **SetupWriteTextLogInfLine** ，具体取决于系统定义的日志令牌值。

    有关日志令牌的详细信息，请参阅 [设置和获取线程的日志令牌](setting-and-getting-a-log-token-for-a-thread.md)。

-   一个标志值，它是系统定义的常量的按位 "或"，用于指定事件级别、缩进深度以及是否包含时间戳。 [设置文本日志的事件级别](setting-the-event-level-for-a-text-log.md)中介绍了事件级别。

    如果为文本日志设置的事件级别大于或等于项的事件级别，则 [**SetupWriteTextLogInfLine**](/windows/win32/api/setupapi/nf-setupapi-setupwritetextloginfline) 会在文本日志中写入日志项。 否则， **SetupWriteTextLogInfLine** 不会在文本日志中写入日志项。 通过使用缩进，可以排列经过格式的消息，使节中的信息更易于阅读和理解。

    有关详细信息，请参阅 [写入缩进的日志条目](writing-indented-log-entries.md)。

-   包含 INF 文件行的 INF 文件的句柄。

-   INF 文件行的上下文。

**SetupWriteTextLogInfLine** 写入以下格式的日志条目：

*entry_prefix time_stamp* **inf：**<em>缩进 inf 文本文件</em> ** (** <em>inf-文件名</em>**行**<em>号</em>**) **

其中：

-   *Entry_prefix*、*时间戳*和*缩进*字段与[文本日志节正文的格式](format-of-a-text-log-section-body.md)中所述的字段相同。

-   **Inf：** 字段指定 TXTLOG_INF 事件类别。 事件类别在 [启用文本日志的事件类别](enabling-event-categories-for-a-text-log.md)中进行了介绍。

-   " *Inf-行文本* " 字段包含指定的 inf 文件行的文本。

-   *Inf-文件名*字段包含包含指定 inf 文件行的 inf 文件的名称。

-   " **行** " 字段指示后面的内容是 INF 文件中的行号。

-   *行号*字段包含 INF 文件中指定行的行号。

下面的示例演示应用程序通常如何在文本日志中记录 INF 行的文本。 本示例中的 INF 行是一个 INF **AddReg** 行。 应用程序调用 [**SetupWriteTextLogInfLine**](/windows/win32/api/setupapi/nf-setupapi-setupwritetextloginfline)，并提供以下输入参数值：

-   *LogToken* 设置为 [**SetupGetThreadLogToken**](/windows/win32/api/setupapi/nf-setupapi-setupgetthreadlogtoken) 返回的日志令牌，或设置为系统定义的 [日志令牌](log-tokens.md)。

-   *LogFlags* 设置为 TXTLOG_DETAILS。 此示例不包含时间戳或更改缩进深度。 在此示例中，缩进深度为五个等宽文本空间。

-   *InfHandle* 设置为 inf 文件 hidserv 的句柄 *。* 此句柄是通过调用平台 SDK 中记录的 **SetupOpenInfFile** 函数获取的。

-   *上下文* 设置为 inf 文件行的 inf 文件上下文，其中包含文本 "AddReg = HidServ_AddService_AddReg"。 可以通过调用 **SetupFind*Xxx*line** 函数（在平台 SDK 中进行了介绍）获取行的 INF 文件上下文。

*LogToken*和*LogFlags*的值会影响[**SetupWriteTextLogInfLine**](/windows/win32/api/setupapi/nf-setupapi-setupwritetextloginfline)的操作，其方式与对[**SetupWriteTextLog**](/windows/win32/api/setupapi/nf-setupapi-setupwritetextlog)所述的方式相同。 此外， **SetupWriteTextLogInfLine** 使用 TXTLOG_INF 的事件目录。

在此示例中，下面显示了 **SetupWriteTextLogInfLine** 写入文本日志的日志项的类型：

```cpp
   inf:      AddReg=HidServ_AddService_AddReg  (hidserv.inf line 98)
```

 

