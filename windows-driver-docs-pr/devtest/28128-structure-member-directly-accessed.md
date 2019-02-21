---
title: C28128
description: 警告 C28128 对字段的访问权限进行直接。 它应该是通过例程。
ms.assetid: 66b3345b-fab8-4f1a-b7ab-dfc5e70ca312
keywords:
- 警告列出 WDK PREfast for Drivers
- 错误列出 WDK PREfast for Drivers
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28128
ms.openlocfilehash: 9ad8ed3909536efc44c68a345df069915ebd049b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523239"
---
# <a name="c28128"></a>C28128


警告 C28128:已直接进行访问的字段。 它应该是通过例程。

该驱动程序直接访问应仅通过使用专用的函数访问的结构成员。

例如，应使用[ **IoSetCancelRoutine** ](https://msdn.microsoft.com/library/windows/hardware/ff549674)而不是直接修改**CancelRoutine**隶属[ **IRP** ](https://msdn.microsoft.com/library/windows/hardware/ff550694)结构。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>示例

下面的代码示例会引起此警告。

```
irp->CancelRoutine = myCancelRoutine;
```

下面的代码示例可避免此警告。

```
oldCancel = IoSetCancelRoutine(irp, myCancelRoutine);
```

 

 





