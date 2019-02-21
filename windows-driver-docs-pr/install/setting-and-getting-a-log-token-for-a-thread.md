---
title: 设置和获取日志标记线程
description: 设置和获取日志标记线程
ms.assetid: 6c701b91-ae0a-48ba-a1e0-711fc21eaf60
keywords:
- 文本日志 WDK SetupAPI，日志上下文
- 日志上下文 WDK SetupAPI
- SetupGetThreadLogToken
- SetupAPI 日志记录 WDK Windows Vista 中，日志上下文
- 记录令牌 WDK SetupAPI
- 线程日志令牌 WDK SetupAPI
- SetupSetThreadLogToken
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8fd984a1cda789acb583c4a570992a92e9ab8c26
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524008"
---
# <a name="setting-and-getting-a-log-token-for-a-thread"></a>设置和获取日志标记线程


[SetupAPI 日志记录](setupapi-logging--windows-vista-and-later-.md)支持建立一个线程的日志上下文的机制。 通过设置来建立此上下文[日志令牌](log-tokens.md)线程。 安装程序 Api 提供这种机制，以便由线程调用的代码可以将日志项写入日志上下文调用线程。

例如，一个线程可以调用类安装程序或辅助安装程序之前设置其日志的上下文的日志标记。 安装程序中，反过来，可以检索调用线程的日志令牌，并使用该令牌中的文本日志和与调用线程的日志上下文关联的部分来写入日志项。

### <a href="" id="setting-a-log-token-for-a-thread"></a> 设置线程的日志令牌

[ **SetupSetThreadLogToken** ](https://msdn.microsoft.com/library/windows/hardware/ff552216)函数将设置从其调用此函数的线程的日志标记。 日志标记可以是系统定义的日志令牌或通过调用检索到的日志标记[ **SetupGetThreadLogToken**](https://msdn.microsoft.com/library/windows/hardware/ff552211)。

如何为线程建立日志上下文的示例如下：

-   安装应用程序可以调用**SetupSetThreadLogToken**来建立日志上下文的程序在同一线程中运行其他安装代码。 如果它建立一个线程的日志上下文，应用程序应使用系统定义[日志令牌](log-tokens.md)，如 LOGTOKEN_SETUPAPI_APPLOG，在调用**SetupSetThreadLogToken**。

    **请注意**  使用系统定义设置的日志上下文[日志标记](log-tokens.md)，后续调用[SetupAPI 日志记录函数](https://msdn.microsoft.com/library/windows/hardware/ff550878)从该日志上下文所做的写入日志安装文本日志，这不是项的一部分[文本日志部分](format-of-a-text-log-section.md)。

     

-   如果类安装程序或辅助安装程序启动新线程，则安装程序可以设置该线程是与父线程相同的日志上下文。 这是通过以下方式：
    1.  父线程启动新线程之前，它将获取当前日志令牌通过调用[ **SetupGetThreadLogToken**](https://msdn.microsoft.com/library/windows/hardware/ff552211)。
    2.  父线程启动新线程，并将当前日志令牌传递通过特定于实现的方法，如将令牌保存在全局变量。
    3.  新的线程调用[ **SetupSetThreadLogToken** ](https://msdn.microsoft.com/library/windows/hardware/ff552216)与当前日志标记。 新线程结果，"继承"的父线程日志上下文。

    **请注意**  如果类安装程序或辅助安装程序的线程设置通过使用此方法中，对后续调用日志上下文[SetupAPI 日志记录函数](https://msdn.microsoft.com/library/windows/hardware/ff550878)从该日志上下文写入日志项所做的安装可能属于的文本日志[文本日志部分](format-of-a-text-log-section.md)。 只有文本日志部分所建立的名为安装程序安装程序 Api 安装操作时，才会出现此问题。

     

以下是对的调用示例**SetupSetThreadLogToken**的当前线程的日志上下文设置为设备安装文本日志 (*SetupAPI.app.log)* 通过指定LOGTOKEN_SETUPAPI_APPLOG 的系统定义的日志标记。 随后调用[SetupAPI 日志记录函数](https://msdn.microsoft.com/library/windows/hardware/ff550878)，使用此上下文中日志会写入日志条目写入设备安装文本日志，但不是作为的一部分[文本日志部分](format-of-a-text-log-section.md)。

```cpp
SP_LOG_TOKEN LogToken = LOGTOKEN_SETUPAPI_APPLOG;
SetupSetThreadLogToken(LogToken);
```

### <a href="" id="getting-a-log-token-for-a-thread"></a> 获取一个线程令牌日志

[ **SetupGetThreadLogToken** ](https://msdn.microsoft.com/library/windows/hardware/ff552211)函数检索从其调用此函数的线程的日志标记。

例如，可以调用类安装程序**SetupGetThreadLogToken**检索适用于名为类安装程序的安装程序 Api 操作的日志标记。 类安装程序然后可以使用此检索的日志令牌适用于相应的安装程序 Api 操作的文本日志中的日志条目。

**请注意**  如果调用不之前设置线程的日志上下文[ **SetupSetThreadLogToken**](https://msdn.microsoft.com/library/windows/hardware/ff552216)，调用**SetupGetThreadLogToken**返回值为 LOGTOKEN_UNSPECIFIED 日志标记。

 

以下是对的调用示例**SetupGetThreadLogToken** ，检索当前线程的日志标记。

```cpp
SP_LOG_TOKEN LogToken = SetupGetThreadLogToken();
```

 

 





