---
title: C28143
description: 调用的警告 C28143 的调度例程也必须返回 STATUS_PENDING。
ms.assetid: 3b9e6c4f-73d1-4abc-9495-85bb56e2532b
keywords:
- 警告列出 WDK PREfast for Drivers
- 错误列出 WDK PREfast for Drivers
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28143
ms.openlocfilehash: 8ceebf56e2341a885d11d11416ecc4c2e748259a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361585"
---
# <a name="c28143"></a>C28143


警告 C28143:调用的调度例程也必须返回状态\_PENDING

调用的调度例程[ **IoMarkIrpPending** ](https://msdn.microsoft.com/library/windows/hardware/ff549422)包括驱动程序将返回状态以外的值在其中至少一个路径\_PENDING。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>示例

下面的代码示例会引起此警告。

```
IoMarkIrpPending(Irp);
...
return STATUS_SUCCESS;
```

下面的代码示例可避免此警告。

```
IoMarkIrpPending(Irp);
...
return STATUS_PENDING;
```

 

 





