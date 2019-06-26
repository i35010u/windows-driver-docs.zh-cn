---
title: 调用 SetupWriteTextLogError
description: 调用 SetupWriteTextLogError
ms.assetid: 55edc72a-2d53-4084-a1e4-e7e6515a4990
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6a217ccd807c5903c1affb9ed2a0e66b0d280814
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385287"
---
# <a name="calling-setupwritetextlogerror"></a>调用 SetupWriteTextLogError


[**SetupWriteTextLogError** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupwritetextlogerror)会将信息写入特定于安装程序 Api 的错误或 Win32 错误到有关[SetupAPI 文本日志](setupapi-text-logs.md)。 **SetupWriteTextLogError**将两个连续的条目写入到文本日志： 第一个条目包含相同的信息与写入的相同的格式[ **SetupWriteTextLog** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupwritetextlog)和第二个条目记录对应的错误代码和错误的用户友好说明。

若要调用**SetupWriteTextLogError**，应用程序提供了它将提供要调用的相同信息**SetupWriteTextLog**和，此外，将提供特定于安装程序 Api 的错误的值或Win32 错误。

**SetupWriteTextLogError**将第一个日志条目写入采用以下格式：

*entry_prefix time_stamp 类别* * * * 格式的缩进-消息 *

**SetupWriteTextLogError**将第二个日志条目写入采用以下格式：

*entry_prefix time_stamp 类别* * *<strong>* 缩进 * **错误：</strong>* 错误号错误-说明 *

其中：

-   *Entry_prefix*，*时间戳*，*类别*，*缩进*，并*格式化消息*字段是与中所述的相同[格式的文本日志部分正文](format-of-a-text-log-section-body.md)。

-   *错误号*字段包含错误号。

-   *错误说明*字段包含错误的用户友好说明。

下面的示例演示如何应用程序通常可能调用[ **SetupWriteTextLogError** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupwritetextlogerror)文本日志中记录有关错误的信息。 示例中使用的错误是系统启动错误。 应用程序调用**SetupWriteTextLogError**，提供以下参数值：

- *LogToken*设置为一个日志令牌值，该值可以通过调用获得[ **SetupGetThreadLogToken** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupgetthreadlogtoken)或者是系统定义的日志之一中所述的令牌值[登录令牌](log-tokens.md)。

- *类别*设置为 TXTLOG_VENDOR，指示该日志条目由供应商提供的应用程序。 事件类别中所述[启用文本日志的事件类别](enabling-event-categories-for-a-text-log.md)。

- *LogFlags*设置为 TXTLOG_ERROR。 此示例不包括时间戳或更改缩进深度。 当前的缩进深度之前被设置为五个等宽字体的文本空间。 有关如何更改缩进深度信息，请参阅[写入缩进日志条目](writing-indented-log-entries.md)。 事件级别中所述[事件级别设置为文本日志](setting-the-event-level-for-a-text-log.md)。

- *错误*设置为 ERROR_SERVICE_ALREADY_RUNNING 的 Win32 错误代码的值。 此错误代码的十进制值是 1056年。

- *MessageStr 是*设置为文本 ("启动服务：未能启动服务 SomeService")。

- 未提供以逗号分隔参数列表<em>。</em>

参数*LogToken*，*类别*，并*LogFlags*影响的操作**SetupWriteTextLogError**与相同的方式这些参数影响的操作**SetupWriteTextLog**。

下面的代码调用[ **SetupWriteTextLogError** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupwritetextlogerror)编写此示例中的日志条目：

```cpp
//The LogToken value was previously returned by call to
//SetupGetThreadLogToken or one of the system-defined log token values
DWORD Category = TXTLOG_VENDOR; 
DWORD Flags = TXTLOG_ERROR ;
DWORD ErrorCode = 1056; // The corresponding Win32 error code

SetupWriteTextLog(LogToken, Category, Flags, ErrorCode, TEXT("Start Service: Failed to start service 'SomeService'"),);
```

如果 TXTLOG_VENDOR 事件类别，并为文本日志设置 TXTLOG_ERROR 事件级别，此代码会在将按如下所示设置格式的文本日志中创建一个条目：

```cpp
!!!     :  Start Service: Failed to start service 'SomeService' 
!!!   :  Error 1056: An instance of the service is already running.
```

请注意， **SetupWriteTextLogError**提供的字符串"的服务实例已开始运行。" 若要描述其值是 1056年了 Win32 错误。

 

 





