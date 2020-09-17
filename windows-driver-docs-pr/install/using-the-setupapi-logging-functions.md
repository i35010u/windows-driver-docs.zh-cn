---
title: 使用 SetupAPI 日志记录函数
description: 使用 SetupAPI 日志记录函数
ms.assetid: a2ba0da4-b891-4ff9-827b-0d64a7a02c0d
keywords:
- Setupapi.log 日志记录 WDK Windows Vista，函数
- 函数 WDK Setupapi.log
- 文本日志 WDK Setupapi.log，函数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 06029607344dd8152a21304be0727c0ce31acd7b
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90717568"
---
# <a name="using-the-setupapi-logging-functions"></a>使用 SetupAPI 日志记录函数


Setupapi.log 支持安装应用程序、类安装程序和共同安装程序可用于在 Setupapi.log 文本日志中写入日志项的功能，如下所示：

-   若要在 [setupapi.log 文本日志](setupapi-text-logs.md)中写入日志项，安装应用程序将调用 [**SetupWriteTextLog**](/windows/win32/api/setupapi/nf-setupapi-setupwritetextlog)、 [**SetupWriteTextLogError**](/windows/win32/api/setupapi/nf-setupapi-setupwritetextlogerror)或 [**SetupWriteTextLogInfLine**](/windows/win32/api/setupapi/nf-setupapi-setupwritetextloginfline)。 有关如何编写文本日志条目的详细信息，请参阅 [在文本日志中写入日志条目](writing-log-entries-in-a-text-log.md)。

-   Setupapi.log 支持一种机制，用于为线程建立日志上下文。 通过设置线程的日志标记为线程建立日志上下文。 若要为线程设置日志令牌，安装应用程序将调用 [**SetupSetThreadLogToken**](/windows/win32/api/setupapi/nf-setupapi-setupsetthreadlogtoken)。 若要检索线程的日志令牌，安装应用程序将调用 [**SetupGetThreadLogToken**](/windows/win32/api/setupapi/nf-setupapi-setupgetthreadlogtoken)。

    有关日志令牌的详细信息，请参阅 [日志令牌](log-tokens.md)。

    有关如何使用日志令牌的详细信息，请参阅 [设置和获取线程的日志令牌](setting-and-getting-a-log-token-for-a-thread.md)。

 

