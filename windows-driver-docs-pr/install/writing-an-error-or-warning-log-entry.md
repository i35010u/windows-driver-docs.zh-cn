---
title: 写入错误或警告日志条目
description: 写入错误或警告日志条目
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0da80b8085cce557021a7537219129724e86527d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840927"
---
# <a name="writing-an-error-or-warning-log-entry"></a>写入错误或警告日志条目


下面的示例演示应用程序通常如何调用 [**SetupWriteTextLog**](/windows/win32/api/setupapi/nf-setupapi-setupwritetextlog) ，以便在 [setupapi.log 文本日志](setupapi-text-logs.md)中写入错误或警告条目。 但是，如果事件与 Setupapi.log 特定的错误或 Win32 错误相关联，则应用程序可以改为调用 [**SetupWriteTextLogError**](/windows/win32/api/setupapi/nf-setupapi-setupwritetextlogerror) 。 **SetupWriteTextLogError** 便于记录和解释有关这些类型的错误的信息。

有关调用 **SetupWriteTextLog** 记录错误消息的信息，请参阅 [记录错误消息](#logging-an-error-message) 和有关调用 **SetupWriteTextLog** 以记录警告消息的信息，请参阅 [记录警告消息](#logging-a-warning-message)。

### <a name="logging-an-error-message"></a><a href="" id="logging-an-error-message"></a> 记录错误消息

在此示例中，应用程序调用 [**SetupWriteTextLog**](/windows/win32/api/setupapi/nf-setupapi-setupwritetextlog)，并提供以下参数值：

-   *LogToken* 设置为一个日志令牌值，该值可以通过调用 [**SetupGetThreadLogToken**](/windows/win32/api/setupapi/nf-setupapi-setupgetthreadlogtoken) 获取，也可以是 [日志](log-tokens.md)令牌中描述的系统定义的日志令牌值之一。

-   "*类别*" 设置为 "TXTLOG_VENDOR"，指示日志条目由供应商提供的应用程序发出。 事件类别在 [启用文本日志的事件类别](enabling-event-categories-for-a-text-log.md)中进行了介绍。

-   *Flags* 设置为 TXTLOG_ERROR 和 TXTLOG_TIMESTAMP 的按位 "或"。 在此示例中，不更改缩进深度，当前缩进深度之前设置为五个等宽文本空间。 有关如何更改缩进深度的信息，请参阅 [写入缩进的日志条目](writing-indented-log-entries.md)。 " [设置文本日志的事件级别](setting-the-event-level-for-a-text-log.md) " 主题中介绍了事件级别。

-   *MessageStr* 设置为 "应用程序错误 (% d) " )  ( 文本。

-   逗号分隔的列表提供变量错误代码。

下面的代码调用 [**SetupWriteTextLog**](/windows/win32/api/setupapi/nf-setupapi-setupwritetextlog) 为此示例编写日志条目：

```cpp
//The LogToken value was previously returned by call to
//SetupGetThreadLogToken or one of the system-defined log token values
DWORD Category = TXTLOG_VENDOR; 
DWORD Flags = TXTLOG_ERROR | TXTLOG_TIMESTAMP;
DWORD ErrorCode = 1111; // An error code value

SetupWriteTextLog(LogToken, Category, Flags, TEXT("Application Error (%d)"),ErrorCode);
```

如果启用了 TXTLOG_VENDOR 事件类别并且为文本日志设置了 TXTLOG_ERROR 事件级别，则此代码将在文本日志中创建一个条目，格式如下：

```cpp
!!!  2005/02/13 22:06:28.109:    :  Application error (1111) 
```

*Entry_prefix* 字段 "!!! "指示日志条目是一条错误消息。

### <a name="logging-a-warning-message"></a><a href="" id="logging-a-warning-message"></a> 记录警告消息

记录警告消息与记录错误消息几乎完全相同。 不同之处在于事件级别的设置。 将 *标志* 设置为 TXTLOG_WARNING 而不是 TXTLOG_ERROR。 如果按 [记录错误消息](#logging-an-error-message)中所述方式调用 **SetupWriteTextLog** ，则除了 *Flags* 设置为 TXTLOG_WARNING 和 TXTLOG_TIMESTAMP 的按位 "或"， [**SetupWriteTextLog**](/windows/win32/api/setupapi/nf-setupapi-setupwritetextlog)将写入以下日志条目：

```cpp
!  2005/02/13 22:06:28.109:    :  Application error (1111) 
```

日志条目的 " *entry_prefix* " 字段为 "！ "，它指示这是一条警告消息，而不是"!!! "，它将指示一条错误消息。

 

