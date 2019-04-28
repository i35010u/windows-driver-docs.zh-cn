---
title: 写入错误或警告日志条目
description: 写入错误或警告日志条目
ms.assetid: 80393368-7430-46ca-a53e-c94b7e8acfa0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 35a60e9ec98226c5bfcea29ca6397d623c1aea2a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339228"
---
# <a name="writing-an-error-or-warning-log-entry"></a>写入错误或警告日志条目


下面的示例演示如何应用程序通常可能调用[ **SetupWriteTextLog** ](https://msdn.microsoft.com/library/windows/hardware/ff552218)编写错误或警告中的条目[SetupAPI 文本日志](setupapi-text-logs.md)。 但是，如果事件是与特定于安装程序 Api 的错误或 Win32 错误相关联，则应用程序可以调用[ **SetupWriteTextLogError** ](https://msdn.microsoft.com/library/windows/hardware/ff552232)相反。 **SetupWriteTextLogError**便于进行日志记录和解释这些类型的错误有关的信息。

有关调用信息**SetupWriteTextLog**若要记录一条错误消息，请参阅[日志记录一条错误消息](#logging-an-error-message)以及有关调用**SetupWriteTextLog**到日志一条警告消息，请参阅[日志记录一条警告消息](#logging-a-warning-message)。

### <a href="" id="logging-an-error-message"></a> 日志记录一条错误消息

在此示例中，应用程序调用[ **SetupWriteTextLog**](https://msdn.microsoft.com/library/windows/hardware/ff552218)，提供以下参数值：

-   *LogToken*设置为一个日志令牌值，该值可以通过调用获得[ **SetupGetThreadLogToken** ](https://msdn.microsoft.com/library/windows/hardware/ff552211)或者是系统定义的日志之一中所述的令牌值[登录令牌](log-tokens.md)。

-   *类别*设置为 TXTLOG_VENDOR，指示该日志条目由供应商提供的应用程序。 事件类别中所述[启用文本日志的事件类别](enabling-event-categories-for-a-text-log.md)。

-   *标志*设置为按位或的 TXTLOG_ERROR 和 TXTLOG_TIMESTAMP。 在此示例中，不会更改缩进深度和当前的缩进深度之前被设置为五个等宽字体的文本空间。 有关如何更改缩进深度信息，请参阅[写入缩进日志条目](writing-indented-log-entries.md)。 事件级别中所述[事件级别设置为文本日志](setting-the-event-level-for-a-text-log.md)主题。

-   *MessageStr*设置为文本 （"应用程序错误 (%d)"）。

-   以逗号分隔列表提供了变量的错误代码。

下面的代码调用[ **SetupWriteTextLog** ](https://msdn.microsoft.com/library/windows/hardware/ff552218)编写此示例中的日志项：

```cpp
//The LogToken value was previously returned by call to
//SetupGetThreadLogToken or one of the system-defined log token values
DWORD Category = TXTLOG_VENDOR; 
DWORD Flags = TXTLOG_ERROR | TXTLOG_TIMESTAMP;
DWORD ErrorCode = 1111; // An error code value

SetupWriteTextLog(LogToken, Category, Flags, TEXT("Application Error (%d)"),ErrorCode);
```

如果 TXTLOG_VENDOR 事件类别，并为文本日志设置 TXTLOG_ERROR 事件级别，此代码会在将按如下所示设置格式的文本日志中创建一个条目：

```cpp
!!!  2005/02/13 22:06:28.109:    :  Application error (1111) 
```

*Entry_prefix*字段"!!! -指示日志条目是一条错误消息。

### <a href="" id="logging-a-warning-message"></a> 日志记录一条警告消息

日志记录一条警告消息是几乎与日志记录一条错误消息。 不同之处是事件级别的设置。 设置*标志*而不是 TXTLOG_ERROR TXTLOG_WARNING 到。 如果**SetupWriteTextLog**调用中所述[日志记录一条错误消息](#logging-an-error-message)，只不过*标志*设置为按位或的 TXTLOG_WARNING 和 TXTLOG_TIMESTAMP， [**SetupWriteTextLog** ](https://msdn.microsoft.com/library/windows/hardware/ff552218)应编写以下日志条目：

```cpp
!  2005/02/13 22:06:28.109:    :  Application error (1111) 
```

*Entry_prefix*日志条目的字段是"！ "，指示这是一条警告消息，而不是"!!! "，指示一条错误消息。

 

 





