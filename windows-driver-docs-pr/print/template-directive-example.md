---
title: 模板指令示例
description: 模板指令示例
ms.assetid: ae8fe5e6-ee79-424d-80b3-fd6300257977
keywords:
- 生产指令 WDK GDL
- 模板 WDK GDL，示例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: db3eac1e8b9dbb3de2b258738552d21c040a2755
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388051"
---
# <a name="template-directive-example"></a>模板指令示例


下面的示例显示了简单的生产环境。

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

通过此生产绑定到主机模板构造实例可以包含任何以下组合：

-   默认值的任何实例\_选择加入或泛型\_选项。

-   一个或多个实例的泛型\_选项，默认值的任何实例\_选择加入。

-   一个或多个实例的泛型\_选项和一个或多个实例的默认\_选择加入。

-   构造实例不能有默认值的一个或多个实例\_没有通用的至少一个实例选择\_选项。

如果主机模板继承自其他模板，继承的模板中定义生产还计算，并且还必须是 **，则返回 TRUE**主机模板的计算结果为中生产**TRUE**.

 

 




