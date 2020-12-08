---
title: C28652
description: 警告 C28652 静态初始值设定项导致在写入页上复制，因为有重载的按位运算符。
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28652
ms.openlocfilehash: 64e24fadba84916f45d20f503cece03811a72936
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96794017"
---
# <a name="c28652"></a>C28652


警告 C28652：由于重载的按位运算符，静态初始值设定项导致写入页上的副本

全局或静态 const 变量的静态初始值设定项通常可以在编译时完全计算，因此可以在 rdata 节中生成。 但是，如果任何初始值设定项需要函数调用，则可以将整个初始值设定项置于 "写入时复制" 页，这会产生性能开销。 此初始化操作对枚举类型调用了重载的按位运算符。 如果重载的实现具有明显语义，则使用适当的强制转换或宏可以生成相同的效果，而无需写入复制。

## <a name="span-idexamplespanspan-idexamplespanspan-idexamplespanexample"></a><span id="Example"></span><span id="example"></span><span id="EXAMPLE"></span>实例


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









