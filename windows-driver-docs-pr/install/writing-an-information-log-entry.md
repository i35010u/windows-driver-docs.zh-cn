---
title: 写入信息日志条目
description: 写入信息日志条目
ms.assetid: 624d2a3e-2a11-47fd-941e-1ab59e299821
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d4b409e86f9f434f9e7e142f02e05fd87570dbba
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90717484"
---
# <a name="writing-an-information-log-entry"></a>写入信息日志条目


下面的示例演示应用程序通常如何调用 [**SetupWriteTextLog**](/windows/win32/api/setupapi/nf-setupapi-setupwritetextlog) ，以便在 [setupapi.log 文本日志](setupapi-text-logs.md) 中写入不是警告消息或错误消息的信息项。

有关调用 **SetupWriteTextLog** 记录错误消息的信息，请参阅 [调用 SetupWriteTextLog 记录错误或警告条目](writing-an-error-or-warning-log-entry.md)。

应用程序调用 [**SetupWriteTextLog**](/windows/win32/api/setupapi/nf-setupapi-setupwritetextlog)，并提供以下参数值：

-   *LogToken* 设置为一个日志令牌值，该值可以通过调用 [**SetupGetThreadLogToken**](/windows/win32/api/setupapi/nf-setupapi-setupgetthreadlogtoken) 获取，也可以是 [日志](log-tokens.md)令牌中描述的系统定义的日志令牌值之一。

-   "*类别*" 设置为 "TXTLOG_VENDOR"，指示日志条目由供应商提供的应用程序发出。 事件类别在 [启用文本日志的事件类别](enabling-event-categories-for-a-text-log.md)中进行了介绍。

-   *Flags* 设置为 TXTLOG_DETAILS 和 TXTLOG_TIMESTAMP 的按位 "或"。 在此示例中，不更改缩进深度，当前缩进深度之前设置为五个等宽文本空间。 有关如何更改缩进深度的信息，请参阅 [写入缩进的日志条目](writing-indented-log-entries.md)。 " [设置文本日志的事件级别](setting-the-event-level-for-a-text-log.md) " 主题中介绍了事件级别。

-   *MessageStr* 设置为文本 ( "感兴趣的变量： =% d" ) 。

-   逗号分隔的参数列表提供了变量 *SomeVariable*，它对应于 *MessageStr*中的 "% d" 字段。

```cpp
//The LogToken value was previously returned by call to
//SetupGetThreadLogToken or one of the system-defined log token values
DWORD Category = TXTLOG_VENDOR; 
DWORD Flags = TXTLOG_DETAILS | TXTLOG_TIMESTAMP;
DWORD SomeVariable = 1;   // The variable whose value will be logged

SetupWriteTextLog(LogToken, Category, Flags, TEXT("Variable of interest: = %d"), SomeVariable);
```

如果启用了 TXTLOG_VENDOR 事件类别并且为设备安装文本日志设置了 TXTLOG_DETAILS 事件级别，则此代码将采用以下格式在设备安装日志中创建一个条目，其中时间戳将替换为实际时间戳。

```cpp
     2005/02/13 22:06:28.109:    :  Variable of interest: Abc = 1
```

 

