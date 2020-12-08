---
title: C28128
description: 警告 C28128 已直接对字段进行访问。 它应由例程进行。
keywords:
- 列出用于驱动程序的 WDK PREfast 的警告
- 为驱动程序列出的 WDK PREfast 的错误
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28128
ms.openlocfilehash: 3665888952a9d9293527d55aa260cdd20b1dc3b1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840415"
---
# <a name="c28128"></a>C28128


警告 C28128：已直接访问字段。 它应由例程进行。

驱动程序直接访问仅应使用专用函数访问的结构成员。

例如，你应该使用 [**IoSetCancelRoutine**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcancelroutine) ，而不是直接修改 [**IRP**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)结构的 **CancelRoutine** 成员。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>示例

下面的代码示例 elicits 此警告。

```
irp->CancelRoutine = myCancelRoutine;
```

下面的代码示例可避免此警告。

```
oldCancel = IoSetCancelRoutine(irp, myCancelRoutine);
```

 

