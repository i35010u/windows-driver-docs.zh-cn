---
title: C28652
description: 警告 C28652 静态初始值设定项会导致重载的按位运算符由于写入页上的副本。
ms.assetid: 763A7F2E-ABFF-41D2-9077-4F60B8EBD338
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28652
ms.openlocfilehash: 980e92fd2e250ea745a8b1f543614690e25ecf54
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568494"
---
# <a name="c28652"></a>C28652


警告 C28652:静态初始值设定项导致重载的按位运算符由于写入页上的副本

静态初始值设定项的全局或静态的 const 变量可以通常完全在编译时计算，并因此可以在.rdata 部分中生成。 但是，如果任何初始值设定项需要函数调用，整个初始值设定项可能会放在写入时复制页中，其中具有性能成本。 此初始化已调用重载的按位运算符对枚举类型。 如果重载的实现具有明显的语义，使用相应的强制转换或宏可产生而无需写入时复制的相同的效果。

## <a name="span-idexamplespanspan-idexamplespanspan-idexamplespanexample"></a><span id="Example"></span><span id="example"></span><span id="EXAMPLE"></span>示例


下面的代码示例将生成此警告。

```
#include <nt.h>

typedef enum
{
    ENUM_VAL_1 = 0x1,
    ENUM_VAL_2 = 0x2,
    ENUM_VAL_3 = 0x4
} ENUM_VALS;

DEFINE_ENUM_FLAG_OPERATORS(ENUM_VALS);

const ENUM_VALS rgValsRuntime[] = {
    ENUM_VAL_1 | ENUM_VAL_2,    // Runtime init!
    ENUM_VAL_3                  // Compile time init
};  
```

下面的代码示例可避免此警告。

```
#include <nt.h>

typedef enum
{
    ENUM_VAL_1 = 0x1,
    ENUM_VAL_2 = 0x2,
    ENUM_VAL_3 = 0x4
} ENUM_VALS;

DEFINE_ENUM_FLAG_OPERATORS(ENUM_VALS);

const ENUM_VALS rgValsRuntime[] = {
    (ENUM_VALS) COMPILETIME_OR_2FLAGS(ENUM_VAL_1, ENUM_VAL_2),
    ENUM_VAL_3                  // Compile time init
};
```









