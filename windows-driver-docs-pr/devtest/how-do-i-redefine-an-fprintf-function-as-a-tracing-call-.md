---
title: 如何重新 fprintf 函数定义为跟踪调用
description: 如何重新 fprintf 函数定义为跟踪调用
ms.assetid: def82d48-454b-421b-a63d-695dae733fd0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 98a9ca30dca368e7bf167f3eaf94a61324b0f74c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519353"
---
# <a name="how-do-i-redefine-an-fprintf-function-as-a-tracing-call"></a>如何重新 fprintf 函数定义为跟踪调用


**Fprintf**最终转换为函数调用**sprintf**函数调用中，是 perceptibly，会降低性能，尤其是在使用它的非常耗费资源的调用重复。

重新定义**fprintf**函数，跟踪调用是高效得多，因为跟踪消息存储在二进制格式和格式设置将推迟到显示的跟踪日志。

若要重新定义的打印函数如**fprintf**作为跟踪调用，生成的调用必须做两件事：

-   分配跟踪功能，例如错误、 警告或干扰的默认级别。

-   忽略该句柄。

下面的示例显示了可同时做到这函数说明：

```
-func:fprintf{LEVEL=Noise}(NULL,MSG,...)
```

可以在本地配置文件中，如 localwpp.ini，定义此函数描述或使用 **-func**参数运行\_WPP （调用 WPP 预处理器宏） 定义的函数说明。

有关运行的可选参数的完整列表\_WPP，请参阅[WPP 预处理器](wpp-preprocessor.md)。

 

 





