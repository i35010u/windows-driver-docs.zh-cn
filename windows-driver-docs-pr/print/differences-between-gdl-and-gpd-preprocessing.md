---
title: GDL 与 GPD 预处理之间的差异
description: GDL 与 GPD 预处理之间的差异
keywords:
- GPD 文件条目 WDK Unidrv，预处理器指令
- GPD 文件条目 WDK Unidrv，与 GDL 文件条目
- GDL WDK，vs GPD
- 预处理器指令 WDK GDL，与 GDL 预处理
- 指令 WDK GDL，源文件预处理器指令
- 源文件 WDK GDL，预处理器指令
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c2e0ecdea4b28fbce4fae83f7d3b8334967d71e5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797213"
---
# <a name="differences-between-gdl-and-gpd-preprocessing"></a>GDL 与 GPD 预处理之间的差异


GDL 中有四个新的预处理器指令，它们在 GPD 实现中不存在： **\# 预编译**、 **\# UndefinePrefix**、 **\# EnablePPDirective** 和 **\# DisablePPDirective**。

此外，未 **\# 定义** 的指令现在还不接受任何参数。 缺少参数意味着最近定义的符号未定义，这将还原以前定义的符号。

建议你不要使用这些新指令（如果 GDL 文件也可由 GPD 分析器进行分析）。 如果希望 tp 将新的预处理器指令合并到还旨在供 GPD 分析器使用的 GDL 文件中，必须提供备用 (向后兼容性) 路径，以允许较早的预处理器执行这些新指令。 每个路径都应包含在一个 **\# Ifdef：**、 **\# Else**、 **\# Endif** 构造中，如下面的代码示例所示。

```cpp
#Ifdef: NewParserVersion
*%   Use new preprocessor directives if the parser supports them.
*%   Lock out this entire code path by changing the prefix.
      #SetPPPrefix: #New_
      #New_PreCompiled: ...
      *%  Actually might use a mixture of old and new directives!
      #New_UndefinePrefix:
#Else:
*%  Otherwise only use the original set of directives.
      #OldDirectives: ...
#Endif:
```

此外，在运行新的指令分叉时，应将预处理器前缀设置为不同的内容。 如果分析器遇到错误前缀的指令，则会发出警告。

 

 




