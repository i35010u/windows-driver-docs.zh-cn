---
title: 什么是预发布宏 /
description: 什么是预发布宏 /
ms.assetid: f5acb047-def3-443a-b220-77543f9a71e3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7bb8f0ef4b4af320b1e2b26d836a6d1484fb67e8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56561944"
---
# <a name="what-are-pre--post-macros"></a>什么是 PRE/POST 宏？


预日志记录和后的日志记录宏定义 WPP\_级别\_PRE (*级别*) 和 WPP\_级别\_POST (*级别*) 宏。 后者是扩展的用户代码的一部分的跟踪函数。 前和后的日志记录宏可以用于任何进程内设置或清除跟踪点周围。

默认情况下这些设置不执行任何操作。 但是，您可以定义它们以添加一些预日志记录和后的日志记录的逻辑。

```
PRE macro // If defined
If (WPP_CHECK_INIT && (Level,Flag) is enabled) {
....Call TraceMessage;
}
POST macro // If defined
```

有关如何定义前/后宏的示例，请参阅[方式跟踪-如果使用表达式？](how-are-trace-if-expressions-used-.md)。

 

 





