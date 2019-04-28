---
title: C28715
description: 语义不同的整数类型之间的警告 C28715 强制转换。
ms.assetid: 49e37718-9950-4f63-a554-f924ae8cf0a4
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28715
ms.openlocfilehash: fb82a420c90e0788473346af266a19088adad86b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345861"
---
# <a name="c28715"></a>C28715


警告 C28715:语义不同的整数类型之间强制转换

此警告指示一个布尔值转换为**NTSTATUS**。 这很可能产生意外结果。 例如，返回一个布尔值的函数的典型失败值 (**FALSE**) 是一种成功状态时作为测试**NTSTATUS**。

通常情况下，返回布尔值的函数将返回 1 (对于 **，则返回 TRUE**) 或 0 (对于**FALSE**)。 这两个值被视为由成功代码**NT\_成功**宏。 因此，将永远不会检测失败的情况。

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>示例

PREfast 报告的警告的下面的示例。

```
extern BOOL SomeFunction(void);

if (NT_SUCCESS(SomeFunction())) {
   return 0;
} else {
   return -1;
}
```

下面的示例可避免此错误。

```
extern BOOL SomeFunction(void);

if (SomeFunction() == TRUE) {
   return 0;
} else {
   return -1;
}
```

 

 





