---
title: 调用 SetupWriteTextLogError
description: 调用 SetupWriteTextLogError
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e40f8790e2708592d856ca06a425f3bc9ab5b26e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814371"
---
# <a name="calling-setupwritetextlogerror"></a>调用 SetupWriteTextLogError


[**SetupWriteTextLogError**](/windows/win32/api/setupapi/nf-setupapi-setupwritetextlogerror) 将有关特定于 setupapi.log 的错误或 Win32 错误的信息写入 [setupapi.log 文本日志](setupapi-text-logs.md)。 **SetupWriteTextLogError** 将两个连续条目写入到文本日志中：第一个条目包含的信息的格式与 [**SetupWriteTextLog**](/windows/win32/api/setupapi/nf-setupapi-setupwritetextlog) 编写的格式相同，第二个条目记录对应的错误代码和对错误的用户友好说明。

若要调用 **SetupWriteTextLogError**，应用程序提供与调用 **SetupWriteTextLog** 相同的信息，并且还提供 Setupapi.log 特定错误或 Win32 错误的值。

**SetupWriteTextLogError** 写入以下格式的第一个日志条目：

*entry_prefix time_stamp 类别* * * * * 缩进格式的消息 *

**SetupWriteTextLogError** 按以下格式写入第二个日志条目：

*entry_prefix time_stamp 类别*  **<strong>* 缩进 * **错误：</strong>* 错误-编号错误-说明 *

其中：

-   *Entry_prefix*、*时间戳*、*类别*、*缩进* 和 *格式化消息* 字段与 [文本日志节正文的格式](format-of-a-text-log-section-body.md)中所述的字段相同。

-   *错误* 号字段包含错误号。

-   *错误描述* 字段包含错误的用户友好说明。

下面的示例演示应用程序通常如何调用 [**SetupWriteTextLogError**](/windows/win32/api/setupapi/nf-setupapi-setupwritetextlogerror) 来记录文本日志中有关错误的信息。 示例中使用的错误是系统启动错误。 应用程序调用 **SetupWriteTextLogError**，并提供以下参数值：

- *LogToken* 设置为一个日志令牌值，该值可以通过调用 [**SetupGetThreadLogToken**](/windows/win32/api/setupapi/nf-setupapi-setupgetthreadlogtoken) 获取，也可以是 [日志](log-tokens.md)令牌中描述的系统定义的日志令牌值之一。

- "*类别*" 设置为 "TXTLOG_VENDOR"，指示日志条目由供应商提供的应用程序发出。 事件类别在 [启用文本日志的事件类别](enabling-event-categories-for-a-text-log.md)中进行了介绍。

- *LogFlags* 设置为 TXTLOG_ERROR。 此示例不包含时间戳或更改缩进深度。 当前缩进深度之前设置为五个等宽文本空间。 有关如何更改缩进深度的信息，请参阅 [写入缩进的日志条目](writing-indented-log-entries.md)。 [设置文本日志的事件级别](setting-the-event-level-for-a-text-log.md)中介绍了事件级别。

- *错误* 设置为 Win32 错误代码的值，ERROR_SERVICE_ALREADY_RUNNING。 此错误代码的十进制值为1056。

- *MessageStr* 设置为 TEXT ( "start Service：无法启动服务 ' SomeService '" ) 。

- 未提供以逗号分隔的参数列表<em>。</em>

参数 *LogToken*、 *类别* 和 *LogFlags* 会影响 **SetupWriteTextLogError** 的操作，其方式与这些参数影响 **SetupWriteTextLog** 操作的方式相同。

下面的代码调用 [**SetupWriteTextLogError**](/windows/win32/api/setupapi/nf-setupapi-setupwritetextlogerror) 来编写此示例的日志条目：

```cpp
//The LogToken value was previously returned by call to
//SetupGetThreadLogToken or one of the system-defined log token values
DWORD Category = TXTLOG_VENDOR; 
DWORD Flags = TXTLOG_ERROR ;
DWORD ErrorCode = 1056; // The corresponding Win32 error code

SetupWriteTextLog(LogToken, Category, Flags, ErrorCode, TEXT("Start Service: Failed to start service 'SomeService'"),);
```

如果启用了 TXTLOG_VENDOR 事件类别并且为文本日志设置了 TXTLOG_ERROR 事件级别，则此代码将在文本日志中创建一个条目，格式如下：

```cpp
!!!     :  Start Service: Failed to start service 'SomeService' 
!!!   :  Error 1056: An instance of the service is already running.
```

请注意， **SetupWriteTextLogError** 提供了 "服务的实例已在运行" 字符串。 描述其值为1056的 Win32 错误。

 

