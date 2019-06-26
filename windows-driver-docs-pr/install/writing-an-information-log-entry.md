---
title: 写入信息日志条目
description: 写入信息日志条目
ms.assetid: 624d2a3e-2a11-47fd-941e-1ab59e299821
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 56719940cefae8e5105ddb03d47e1b3b60e484b6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363486"
---
# <a name="writing-an-information-log-entry"></a>写入信息日志条目


下面的示例演示如何应用程序通常可能调用[ **SetupWriteTextLog** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupwritetextlog)若要写入信息条目[SetupAPI 文本日志](setupapi-text-logs.md)，它不是警告消息或错误消息。

有关调用信息**SetupWriteTextLog**若要记录一条错误消息，请参阅[调用 SetupWriteTextLog 来记录错误或警告条目](writing-an-error-or-warning-log-entry.md)。

应用程序调用[ **SetupWriteTextLog**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupwritetextlog)，提供以下参数值：

-   *LogToken*设置为一个日志令牌值，该值可以通过调用获得[ **SetupGetThreadLogToken** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupgetthreadlogtoken)或者是系统定义的日志之一中所述的令牌值[登录令牌](log-tokens.md)。

-   *类别*设置为 TXTLOG_VENDOR，指示该日志条目由供应商提供的应用程序。 事件类别中所述[启用文本日志的事件类别](enabling-event-categories-for-a-text-log.md)。

-   *标志*设置为按位或的 TXTLOG_DETAILS 和 TXTLOG_TIMESTAMP。 在此示例中，不会更改缩进深度和当前的缩进深度之前被设置为五个等宽字体的文本空间。 有关如何更改缩进深度信息，请参阅[写入缩进日志条目](writing-indented-log-entries.md)。 事件级别中所述[事件级别设置为文本日志](setting-the-event-level-for-a-text-log.md)主题。

-   *MessageStr*设置为文本 ("感兴趣的变量: = %d")。

-   以逗号分隔参数列表提供了变量*SomeVariable*，这对应于"%d"字段中*MessageStr*。

```cpp
//The LogToken value was previously returned by call to
//SetupGetThreadLogToken or one of the system-defined log token values
DWORD Category = TXTLOG_VENDOR; 
DWORD Flags = TXTLOG_DETAILS | TXTLOG_TIMESTAMP;
DWORD SomeVariable = 1;   // The variable whose value will be logged

SetupWriteTextLog(LogToken, Category, Flags, TEXT("Variable of interest: = %d"), SomeVariable);
```

如果启用 TXTLOG_VENDOR 事件类别并为设备安装文本日志设置 TXTLOG_DETAILS 事件级别，此代码将采用以下格式，其中的时间戳将替换为实际的设备安装日志中创建条目时间戳。

```cpp
     2005/02/13 22:06:28.109:    :  Variable of interest: Abc = 1
```

 

 





