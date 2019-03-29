---
title: C28616
description: 警告 C28616 多线程 AV 条件。
ms.assetid: 77be6a23-18dc-420c-9359-ab91f216c73b
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28616
ms.openlocfilehash: 5b8809ce32ad3bfb3f88d46b9a627bf5a6f477f7
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57350022"
---
# <a name="c28616"></a>C28616


警告 C28616:多线程的 AV 条件

在多线程环境中，则无法知道当线程被抢占，具有降低对象的引用计数的明显的效果是删除而无需执行当前线程的进一步操作的结果。 引用计数可能存在一定的从零后，应为引用计数对象不能访问。

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>示例

以下是线程可能会公开此问题的时间序列的示例：

线程 T1 执行行 1、 2 和 3，递减**m\_cRef**为 1，并且在被取代。

另一个线程 T2 执行行 1、 2 和 3 递减**m\_cRef**为 0。 然后它将执行行 4 和 5，其中**这**会删除，并且最后执行第 6 行。

当 T1 重新计划任务时，它将引用**m\_cref**第 9 行上。 因此它将在相关的删除此指针后访问的成员变量，且对象堆时处于未知状态。

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

已更正的示例后删除该对象未引用任何堆内存。

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

 

 





