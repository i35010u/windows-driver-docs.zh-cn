---
title: 使用 SetupAPI 日志记录函数
description: 使用 SetupAPI 日志记录函数
ms.assetid: a2ba0da4-b891-4ff9-827b-0d64a7a02c0d
keywords:
- SetupAPI 日志记录 WDK Windows Vista 中，函数
- WDK SetupAPI 函数
- 文本日志 WDK SetupAPI，函数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2a114b1790abe06c0a57947c678e962329bb6026
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384746"
---
# <a name="using-the-setupapi-logging-functions"></a>使用 SetupAPI 日志记录函数


安装程序 Api 还支持安装应用程序、 类的安装程序，以及共同安装程序可用于在 SetupAPI 文本日志中，按如下所示编写日志条目的函数：

-   若要写入日志条目[SetupAPI 文本日志](setupapi-text-logs.md)，安装应用程序调用[ **SetupWriteTextLog**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupwritetextlog)， [ **SetupWriteTextLogError**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupwritetextlogerror)，或[ **SetupWriteTextLogInfLine**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupwritetextloginfline)。 有关如何编写文本日志条目的详细信息，请参阅[文本日志中写入日志条目](writing-log-entries-in-a-text-log.md)。

-   安装程序 Api 支持一种机制来建立日志上下文线程。 通过设置线程的日志标记的线程被建立日志上下文。 若要设置的线程的日志标记，安装应用程序调用[ **SetupSetThreadLogToken**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupsetthreadlogtoken)。 若要检索的线程的日志标记，安装应用程序调用[ **SetupGetThreadLogToken**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupgetthreadlogtoken)。

    有关日志令牌的详细信息，请参阅[日志令牌](log-tokens.md)。

    有关如何使用日志令牌的详细信息，请参阅[设置和获取日志标记线程](setting-and-getting-a-log-token-for-a-thread.md)。

 

 





