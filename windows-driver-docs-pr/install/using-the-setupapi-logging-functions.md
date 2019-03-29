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
ms.openlocfilehash: 9a6d6fe0e7ab9212b359739931bf9be61f45e5bd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567728"
---
# <a name="using-the-setupapi-logging-functions"></a>使用 SetupAPI 日志记录函数


安装程序 Api 还支持安装应用程序、 类的安装程序，以及共同安装程序可用于在 SetupAPI 文本日志中，按如下所示编写日志条目的函数：

-   若要写入日志条目[SetupAPI 文本日志](setupapi-text-logs.md)，安装应用程序调用[ **SetupWriteTextLog**](https://msdn.microsoft.com/library/windows/hardware/ff552218)， [ **SetupWriteTextLogError**](https://msdn.microsoft.com/library/windows/hardware/ff552232)，或[ **SetupWriteTextLogInfLine**](https://msdn.microsoft.com/library/windows/hardware/ff552236)。 有关如何编写文本日志条目的详细信息，请参阅[文本日志中写入日志条目](writing-log-entries-in-a-text-log.md)。

-   安装程序 Api 支持一种机制来建立日志上下文线程。 通过设置线程的日志标记的线程被建立日志上下文。 若要设置的线程的日志标记，安装应用程序调用[ **SetupSetThreadLogToken**](https://msdn.microsoft.com/library/windows/hardware/ff552216)。 若要检索的线程的日志标记，安装应用程序调用[ **SetupGetThreadLogToken**](https://msdn.microsoft.com/library/windows/hardware/ff552211)。

    有关日志令牌的详细信息，请参阅[日志令牌](log-tokens.md)。

    有关如何使用日志令牌的详细信息，请参阅[设置和获取日志标记线程](setting-and-getting-a-log-token-for-a-thread.md)。

 

 





