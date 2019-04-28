---
title: C28716
description: 警告 C28716 编译器插入语义不同的整数类型之间的强制转换。
ms.assetid: 6cb5e57f-3535-4ef2-b586-d46d0de60a4b
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28716
ms.openlocfilehash: 31b8751ef4f1a130c13870ef71456a3ff5b6ec67
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345847"
---
# <a name="c28716"></a>C28716


警告 C28716:编译器插入语义不同的整数类型之间的强制转换

此警告指示一个布尔值正被用作**NTSTATUS**而无需进行显式强制转换。 这很可能产生意外结果。 例如，返回一个布尔值 (false) 的函数的典型失败值指示成功状态时作为测试**NTSTATUS**。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>示例

PREfast 报告的警告的下面的示例。

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

 

 





