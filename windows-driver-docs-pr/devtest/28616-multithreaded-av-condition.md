---
title: C28616
description: 警告 C28616 多线程 AV 情况。
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28616
ms.openlocfilehash: 173f88a30cee4df1a50ec3e6bb3151ccabf2e75f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795639"
---
# <a name="c28616"></a>C28616


警告 C28616：多线程 AV 条件

在多线程环境中，不可能知道线程何时被抢占，这会导致降低对象的引用计数的明显效果是删除，而不会在当前线程中执行其他操作。 在引用计数可能为零时，不能访问引用计数的对象。

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>示例

下面是可能公开此问题的线程时间序列示例：

线程 T1 执行第1、2和3行，将 **m \_ cRef** 减为1，并被抢占。

另一个线程 T2 执行第1、2和3行，将 **m \_ cRef** 减为0。 然后，它将执行第4行和第5行，其中 **删除了，** 最后执行第6行。

当重新计划 T1 时，它将引用第9行的 **m \_ cref** 。 因此，它将在删除相关的指针之后访问成员变量，而当对象的堆处于未知状态时，它将访问该变量。

```
  1 ULONG CObject::Release()
  2 {
  3     if ( 0 == InterlockedDecrement(&m_cRef) )
  4     {
  5         delete this;
  6         return NULL;
  7     }
  8     /* this.m_cRef isn't thread safe */
  9     return m_cRef;
 10 }
```

已更正的示例不在删除对象后引用任何堆内存。

```
ULONG CObject::Release()
{
 ASSERT( 0 != m_cRef );
 ULONG cRef = InterlockedDecrement(&m_cRef);
 if ( 0 == cRef )
 {
 delete this;
 }
 return cRef;
}
```

 

 





