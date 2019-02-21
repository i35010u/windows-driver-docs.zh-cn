---
title: C28753
description: 警告 C28753 信赖未定义参数的计算顺序。
ms.assetid: D8879714-63A2-4F36-B08A-1E487ACB5BC1
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28753
ms.openlocfilehash: f95dcececc7071227dec9f761f0f5af9f2873100
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554851"
---
# <a name="c28753"></a>C28753


警告 C28753:依赖于未定义参数的计算顺序

C/c + + 允许编译器生成代码以计算实际参数按任意顺序和 x86 和 ARM 编译器倾向于选择不同的顺序。 在不同平台上，依赖于特定的顺序的代码的行为可能有所不同。

一个常见错误是通过使用智能指针其中 address-of 运算符**&** 中调用此类还具有负面影响：

```ManagedCPlusPlus
sp->Foo(&sp);
```

对成员访问运算符的调用**- &gt;** and 运算符**&** 按任意顺序可能会发生。 从运算符因此副作用**&** 之前或之后运算符可能会发生这种情况**- &gt;** 调用。 此警告查找这些错误的调用，以防止不同平台之间的行为。

## <a name="span-idexamplespanspan-idexamplespanspan-idexamplespanexample"></a><span id="Example"></span><span id="example"></span><span id="EXAMPLE"></span>示例


下面的示例代码将生成此警告。

```ManagedCPlusPlus
sp->Foo(&sp)
```

下面的代码示例可避免此警告。

```ManagedCPlusPlus
SmartPtr spTemp;
sp->Foo(&spTemp);
sp = spTemp;
```

 

 





