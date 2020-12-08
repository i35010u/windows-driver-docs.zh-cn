---
title: C28715
description: 语义不同的整数类型之间的警告 C28715 转换。
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28715
ms.openlocfilehash: 41ed6a7d48d134b4ba6650397aa72ad209bcde20
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837331"
---
# <a name="c28715"></a>C28715


警告 C28715：语义不同的整数类型之间的强制转换

此警告指示布尔值将转换为 **NTSTATUS**。 这可能会产生意外的结果。 例如，在测试为 **NTSTATUS** 时，返回布尔值的函数的典型失败值 (**FALSE**) 为成功状态。

通常，返回布尔值的函数为 **TRUE**) 返回 1 (; 对于 **FALSE**) ，返回 0 (。 **NT \_ success** 宏会将这两个值视为成功代码。 因此，永远不会检测到故障情况。

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>示例

PREfast 报告以下示例的警告。

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

 

 





