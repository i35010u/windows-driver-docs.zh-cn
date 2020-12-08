---
title: C28753
description: 警告 C28753 依赖未定义的参数计算顺序。
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28753
ms.openlocfilehash: 2dcdd7d9023fcadb81170cce502386af5ae7504e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788757"
---
# <a name="c28753"></a>C28753


警告 C28753：依赖于未定义的参数计算顺序

C/c + + 允许编译器生成代码以按任意顺序计算实际参数，而 x86 和 ARM 编译器倾向于选择不同的顺序。 依赖于特定顺序的代码在不同平台上的行为可能不同。

常见的错误是，使用智能指针，其中的地址运算符 **&** 有副作用，如以下所示：

```ManagedCPlusPlus
sp->Foo(&sp);
```

对成员访问运算符 **-&gt;** 和运算符的调用 **&** 可能会按顺序发生。 因此，可能会在 **&** 调用 operator 之前或之后发生副作用 **-&gt;** 。 此警告会发现这些错误调用，以防平台之间出现不同的行为。

## <a name="span-idexamplespanspan-idexamplespanspan-idexamplespanexample"></a><span id="Example"></span><span id="example"></span><span id="EXAMPLE"></span>实例


下面的代码示例将生成此警告。

```ManagedCPlusPlus
sp->Foo(&sp)
```

下面的代码示例可避免此警告。

```ManagedCPlusPlus
SmartPtr spTemp;
sp->Foo(&spTemp);
sp = spTemp;
```

 

 





