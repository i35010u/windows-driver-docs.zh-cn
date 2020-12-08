---
title: 模板指令示例
description: 模板指令示例
keywords:
- 生产指令 WDK GDL
- 模板 WDK GDL，示例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2f67505cb29f5d4d5375ca590e1c9fb8f4c6afac
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806741"
---
# <a name="template-directive-example"></a>模板指令示例


下面的示例演示一个简单的生产。

```cpp
  *Production: EXACTLY_ONE
  {
        *Production: SATISFY_ALL
        {
            *Member: GENERIC_OPTION {*Occurs: [1-*] }
            *Member: DEFAULT_OPT {*Occurs: [0-*] }
        }
        *Production: SATISFY_ALL
        {
            *Member: GENERIC_OPTION {*Occurs: [0] }
            *Member: DEFAULT_OPT {*Occurs: [0] }
        }
  }
```

此生产绑定到主机模板的构造实例可以包含以下任何组合：

-   默认 \_ OPT 或通用选项没有任何实例 \_ 。

-   泛型选项的一个或多个实例 \_ ，默认值为 \_ OPT 的实例。

-   一个或多个泛型 \_ 选项实例和默认 OPT 的一个或多个实例 \_ 。

-   构造实例不能有一个或多个默认的实例 \_ OPT，无需使用至少一个泛型选项的实例 \_ 。

如果主机模板继承自其他模板，则还会评估在继承的模板中定义的生产，并且还必须为 **true** ，以便主机模板中的生产评估为 **true**。

 

 




