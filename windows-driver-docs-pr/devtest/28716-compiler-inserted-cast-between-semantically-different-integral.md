---
title: C28716
description: 警告 C28716 编译器在语义不同的整数类型之间插入强制转换。
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28716
ms.openlocfilehash: 8befca8c562c57ddb9c39d53316404e8f7dd5792
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837327"
---
# <a name="c28716"></a>C28716


警告 C28716：在语义不同的整数类型之间进行编译器插入的强制转换

此警告表示在没有显式强制转换的情况下，布尔值将用作 **NTSTATUS** 。 这可能会产生意外的结果。 例如，返回布尔值的函数的典型失败值 (false) 在测试为 **NTSTATUS** 时指示成功状态。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>示例

PREfast 报告以下示例的警告。

```
extern bool SomeMemAllocFunction(void **);

return SomeMemAllocFunction(&MyPtr);
```

下面的示例可避免此错误。

```
extern bool SomeMemAllocFunction(void **);

if (SomeMemAllocFunction(&MyPtr) == true) {
 return STATUS_SUCCESS;
} else {
 return STATUS_NO_MEMORY;
}
```

 

 





