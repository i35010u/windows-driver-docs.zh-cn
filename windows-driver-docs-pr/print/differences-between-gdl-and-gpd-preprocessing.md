---
title: GDL 和 GPD 预处理之间的差异
description: GDL 和 GPD 预处理之间的差异
ms.assetid: 0ca79e85-1697-4f8d-b534-fe24748aaf5b
keywords:
- GPD 文件条目 WDK Unidrv，预处理器指令
- GPD 文件条目 WDK Unidrv，vs。GDL 文件条目
- GDL WDK，vs GPD
- 预处理器指令 WDK GDL，vs。GDL 预处理
- 指令 WDK GDL，源文件预处理器指令
- 源文件 WDK GDL，预处理器指令
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 656b294f610e4e65fc03c1cf29da6fafbd8df319
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554220"
---
# <a name="differences-between-gdl-and-gpd-preprocessing"></a>GDL 和 GPD 预处理之间的差异


GPD 实现中不存在的 GDL 中有四个新的预处理器指令：**\#预编译**，  **\#UndefinePrefix**，  **\#EnablePPDirective**，并且 **\#DisablePPDirective**。

此外， **\#未定义**指令现在还接受任何参数。 缺少参数意味着最新定义的符号未定义，这将还原以前定义的符号。

我们建议如果 GDL 文件还应分析 GPD 分析器不会使用这些新指令。 如果你想 tp 合并 GDL 到新的预处理器指令文件还旨在用于通过 GPD 分析器，备用 （向后兼容性） 路径必须提供允许较旧的预处理器，以避免执行这些新指令。 每个路径括起来 **\#Ifdef:**，  **\#Else**，  **\#Endif**构造，如下面的代码示例显示。

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

此外，预处理器前缀应设置为不同运行新的指令分叉时。 分析器会发出警告如果遇到了错误的前缀指令。

 

 




