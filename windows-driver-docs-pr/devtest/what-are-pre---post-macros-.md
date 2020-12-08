---
title: 什么是前置/后宏
description: 什么是前置/后宏
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 83c58c502756605db2f467263cd3e9ccbacd48ae
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810731"
---
# <a name="what-are-pre--post-macros"></a>什么是 PRE/POST 宏？


预日志记录和记录后的宏定义 WPP \_ 级别 \_ (*级别* 的) 和 wpp \_ 级别， \_) 宏之后 (*级别* 。 后者是作为跟踪函数扩展的一部分的用户代码。 预先和后期日志记录宏可用于任何进程内设置或用于跟踪点的清理。

默认情况下，它们设置为 "不执行任何操作"。 不过，您可以将它们定义为添加一些预日志记录和日志记录逻辑。

```
PRE macro // If defined
If (WPP_CHECK_INIT && (Level,Flag) is enabled) {
....Call TraceMessage;
}
POST macro // If defined
```

有关如何定义 PRE/POST 宏的示例，请参阅 [如何使用 Trace-If 表达式？](how-are-trace-if-expressions-used-.md)。

 

 





