---
title: 如何实现将 fprintf 函数重新定义为跟踪调用
description: 如何实现将 fprintf 函数重新定义为跟踪调用
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c6cb6f5a369071e015d7717d069c48e73321a7e8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839125"
---
# <a name="how-do-i-redefine-an-fprintf-function-as-a-tracing-call"></a>如何将 fprintf 函数重新定义为跟踪调用？


**Fprintf** 函数调用最终转换为 **sprintf** 函数调用，这是一项占用大量资源的调用，可能会降低性能 perceptibly，尤其是重复使用它时。

重新定义 **fprintf** 函数作为跟踪调用的效率要高得多，因为跟踪消息是以二进制格式存储的，而格式延迟直到显示跟踪日志。

若要将打印功能（如 **fprintf** ）重新定义为跟踪调用，则生成的调用必须执行两项操作：

-   为跟踪函数分配默认级别，如 "错误"、"警告" 或 "干扰"。

-   忽略句柄。

下面的示例演示了执行这两种操作的函数说明：

```
-func:fprintf{LEVEL=Noise}(NULL,MSG,...)
```

可以在本地配置文件（如 localwpp.ini）中定义此函数说明，或使用 RUN wpp 的 **-func** 参数 \_ (调用 wpp 预处理器) 的宏来定义函数说明。

有关运行 WPP 的可选参数的完整列表 \_ ，请参阅 [WPP 预处理器](wpp-preprocessor.md)。

 

 





