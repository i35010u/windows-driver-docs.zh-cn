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
ms.openlocfilehash: e75da94769aca9ba6a71e49d1494a1e461c90a71
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364133"
---
# <a name="c28128"></a>C28128


警告 C28128:已直接进行访问的字段。 它应该是通过例程。

该驱动程序直接访问应仅通过使用专用的函数访问的结构成员。

例如，应使用[ **IoSetCancelRoutine** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcancelroutine)而不是直接修改**CancelRoutine**隶属[ **IRP** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_irp)结构。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>示例

下面的代码示例会引起此警告。

```
irp->CancelRoutine = myCancelRoutine;
```

下面的代码示例可避免此警告。

```
oldCancel = IoSetCancelRoutine(irp, myCancelRoutine);
```

 

 





