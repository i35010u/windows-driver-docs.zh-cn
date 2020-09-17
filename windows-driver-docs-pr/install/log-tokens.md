---
title: 日志令牌
description: 日志令牌
ms.assetid: f666d457-eb0a-4482-a8ac-e2921ab8c5a9
keywords:
- 日志令牌 WDK Setupapi.log
- 文本日志 WDK Setupapi.log，日志令牌
- 节 WDK Setupapi.log 日志记录
- 标识文本日志节
- Setupapi.log 日志记录 WDK Windows Vista，日志令牌
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1019446f597d3ee3ccbb96a2da83a2d8901fa9c1
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90716352"
---
# <a name="log-tokens"></a>日志令牌


Setupapi.log 文本日志记录使用 *日志令牌* 在 [setupapi.log 文本日志](setupapi-text-logs.md)中写入条目。

类安装程序或共同安装程序必须使用由 [**SetupGetThreadLogToken**](/windows/win32/api/setupapi/nf-setupapi-setupgetthreadlogtoken) 返回的日志令牌来写入 [文本日志节](format-of-a-text-log-section.md) 中的日志项，该部分由调用安装程序的 setupapi.log 安装操作建立。 Setupapi.log 文本日志记录还提供系统定义的日志令牌，安装应用程序可以使用这些令牌来写入不属于文本日志部分的日志项。

Setupapi.log 文本日志记录提供以下系统定义的日志令牌：

<a href="" id="logtoken-unspecified"></a>LOGTOKEN_UNSPECIFIED  
表示不属于 [文本日志部分](format-of-a-text-log-section.md)的未指定文本日志部分。 默认情况下，如果指定了此标记值， [setupapi.log 日志记录函数](/previous-versions/ff550878(v=vs.85)) 将在应用程序安装文本日志中写入日志项。

<a href="" id="logtoken-no-log"></a>LOGTOKEN_NO_LOG  
表示空日志。 如果指定了此标记值，Setupapi.log 日志记录函数将不会写入日志项。

<a href="" id="logtoken-setupapi-applog"></a>LOGTOKEN_SETUPAPI_APPLOG  
表示应用程序文本日志 (不属于文本日志部分的 *setupapi.log) * 部分。 如果指定了此标记值， [setupapi.log 日志记录函数](/previous-versions/ff550878(v=vs.85)) 将在应用程序安装文本日志中写入日志条目。

<a href="" id="logtoken-setupapi-devlog"></a>LOGTOKEN_SETUPAPI_DEVLOG  
表示不属于文本日志部分的设备安装文本日志 (*setupapi.log) * 的一部分。 如果指定了此标记值，Setupapi.log 日志记录函数将在设备安装文本日志中写入日志条目。

 

