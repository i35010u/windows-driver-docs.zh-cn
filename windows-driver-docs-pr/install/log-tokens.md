---
title: 日志标记
description: 日志标记
ms.assetid: f666d457-eb0a-4482-a8ac-e2921ab8c5a9
keywords:
- 记录令牌 WDK SetupAPI
- 文本日志 WDK SetupAPI，日志令牌
- 部分 WDK SetupAPI 日志记录
- 识别的文本日志部分
- SetupAPI 日志记录 WDK Windows Vista 中，日志令牌
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec67e2d57826eb4c16336fc46e50414f2a355eff
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546962"
---
# <a name="log-tokens"></a>日志标记


使用 SetupAPI 文本日志记录*登录令牌*写入条目[SetupAPI 文本日志](setupapi-text-logs.md)。

类安装程序或辅助安装程序必须使用返回的日志令牌[ **SetupGetThreadLogToken** ](https://msdn.microsoft.com/library/windows/hardware/ff552211)写入日志条目[文本日志部分](format-of-a-text-log-section.md)的已建立通过调用安装程序的安装程序 Api 安装操作。 SetupAPI 文本日志记录还提供了系统定义的日志令牌，安装应用程序可用于编写不是文本日志部分的一部分的日志条目。

通过 SetupAPI 文本日志记录提供了以下系统定义的日志标记：

<a href="" id="logtoken-unspecified"></a>LOGTOKEN_UNSPECIFIED  
表示不是未指定的文本日志部分的一部分[文本日志部分](format-of-a-text-log-section.md)。 默认情况下[SetupAPI 日志记录功能](https://msdn.microsoft.com/library/windows/hardware/ff550878)应用程序安装文本日志中写入一个日志条目，如果指定此令牌的值。

<a href="" id="logtoken-no-log"></a>LOGTOKEN_NO_LOG  
表示 null 的日志。 SetupAPI 日志记录功能不写入日志条目如果指定此令牌的值。

<a href="" id="logtoken-setupapi-applog"></a>LOGTOKEN_SETUPAPI_APPLOG  
表示应用程序文本日志的部分 (*SetupAPI.app.log)* ，它不是属于文本日志部分。 [SetupAPI 日志记录功能](https://msdn.microsoft.com/library/windows/hardware/ff550878)应用程序安装文本日志中写入日志项，如果指定此令牌的值。

<a href="" id="logtoken-setupapi-devlog"></a>LOGTOKEN_SETUPAPI_DEVLOG  
表示的一部分的设备安装文本日志 (*SetupAPI.dev.log)* ，它不是属于文本日志部分。 如果指定此令牌的值来 SetupAPI 日志记录功能在设备安装文本日志中写入日志项。

 

 





