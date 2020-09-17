---
title: 设置和获取线程的日志标记
description: 设置和获取线程的日志标记
ms.assetid: 6c701b91-ae0a-48ba-a1e0-711fc21eaf60
keywords:
- 文本日志 WDK Setupapi.log，日志上下文
- 日志上下文 WDK Setupapi.log
- SetupGetThreadLogToken
- Setupapi.log 日志记录 WDK Windows Vista，日志上下文
- 日志令牌 WDK Setupapi.log
- 线程日志令牌 WDK Setupapi.log
- SetupSetThreadLogToken
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 70997832ed26dc0e43986f90319f4fd98ac8a338
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90714896"
---
# <a name="setting-and-getting-a-log-token-for-a-thread"></a>设置和获取线程的日志标记


[Setupapi.log 日志记录](setupapi-logging--windows-vista-and-later-.md) 支持建立线程的日志上下文的机制。 此上下文通过设置线程的 [日志令牌](log-tokens.md) 建立。 Setupapi.log 提供了此机制，以便线程调用的代码可以将日志项写入调用线程的日志上下文。

例如，在调用类安装程序或共同安装程序之前，线程可以为其日志上下文设置日志令牌。 然后，安装程序可检索调用线程的日志令牌，并使用该令牌来写入文本日志中的日志条目以及与调用线程的日志上下文相关联的部分。

### <a name="setting-a-log-token-for-a-thread"></a><a href="" id="setting-a-log-token-for-a-thread"></a> 设置线程的日志标记

[**SetupSetThreadLogToken**](/windows/win32/api/setupapi/nf-setupapi-setupsetthreadlogtoken)函数为从中调用此函数的线程设置日志令牌。 日志标记可以是系统定义的日志令牌，也可以是通过调用 [**SetupGetThreadLogToken**](/windows/win32/api/setupapi/nf-setupapi-setupgetthreadlogtoken)检索到的日志令牌。

以下示例说明了如何为线程建立日志上下文：

-   安装应用程序可以调用 **SetupSetThreadLogToken** 为在同一线程中运行的其他安装代码建立日志上下文。 当它为线程建立日志上下文时，应用程序应在对**SetupSetThreadLogToken**的调用中使用系统定义的[日志令牌](log-tokens.md)，如 LOGTOKEN_SETUPAPI_APPLOG。

    **注意**   如果通过使用系统定义的[日志标记](log-tokens.md)来设置日志上下文，则随后调用从该日志上下文发出的[setupapi.log 日志记录函数](/previous-versions/ff550878(v=vs.85))时，会将日志条目写入到安装文本日志中，这些日志不属于[文本日志部分](format-of-a-text-log-section.md)。

     

-   如果类安装程序或共同安装程序启动新线程，则安装程序可以将该线程的日志上下文设置为与父线程相同。 这可以通过以下方式完成：
    1.  在父线程启动新线程之前，它会通过调用 [**SetupGetThreadLogToken**](/windows/win32/api/setupapi/nf-setupapi-setupgetthreadlogtoken)获取当前日志令牌。
    2.  父线程启动新线程，并通过特定于实现的方法传递当前日志标记，如将令牌保存在全局变量中。
    3.  新线程通过当前日志令牌调用 [**SetupSetThreadLogToken**](/windows/win32/api/setupapi/nf-setupapi-setupsetthreadlogtoken) 。 因此，新线程 "继承" 父线程的日志上下文。

    **注意**   如果类安装程序或共同安装程序的线程通过使用此方法来设置日志上下文，则从该日志上下文中对[setupapi.log 日志记录函数](/previous-versions/ff550878(v=vs.85))进行的后续调用会将日志条目写入到可能是[文本日志部分](format-of-a-text-log-section.md)一部分的安装文本日志中。 这仅在以下情况下发生：文本日志节是通过调用安装程序的 Setupapi.log 安装操作建立的。

     

下面是对 **SetupSetThreadLogToken** 的调用的一个示例，该示例通过指定 LOGTOKEN_SETUPAPI_APPLOG 的系统定义的日志标记将当前线程的日志上下文设置为设备安装文本日志 (*setupapi.log) * 。 对使用此日志上下文的 [setupapi.log 日志记录函数](/previous-versions/ff550878(v=vs.85)) 的后续调用会将日志条目写入设备安装文本日志，而不是作为 [文本日志部分](format-of-a-text-log-section.md)的一部分。

```cpp
SP_LOG_TOKEN LogToken = LOGTOKEN_SETUPAPI_APPLOG;
SetupSetThreadLogToken(LogToken);
```

### <a name="getting-a-log-token-for-a-thread"></a><a href="" id="getting-a-log-token-for-a-thread"></a> 获取线程的日志标记

[**SetupGetThreadLogToken**](/windows/win32/api/setupapi/nf-setupapi-setupgetthreadlogtoken)函数检索从中调用此函数的线程的日志令牌。

例如，类安装程序可以调用 **SetupGetThreadLogToken** 来检索适用于调用类安装程序的 setupapi.log 操作的日志令牌。 然后，类安装程序可以使用此检索到的日志令牌来记录文本日志中应用于相应 Setupapi.log 操作的条目。

**注意**   如果之前未通过调用[**SetupSetThreadLogToken**](/windows/win32/api/setupapi/nf-setupapi-setupsetthreadlogtoken)设置线程的日志上下文，则对**SetupGetThreadLogToken**的调用将返回值为 LOGTOKEN_UNSPECIFIED 的日志令牌。

 

下面是对 **SetupGetThreadLogToken** 的调用的一个示例，它检索当前线程的日志令牌。

```cpp
SP_LOG_TOKEN LogToken = SetupGetThreadLogToken();
```

 

