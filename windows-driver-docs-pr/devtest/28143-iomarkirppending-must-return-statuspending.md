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
ms.openlocfilehash: ce477d3a0df259ad3bfdba86490f6ec70f9e6df0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364123"
---
# <a name="c28143"></a>C28143


警告 C28143:调用的调度例程也必须返回状态\_PENDING

调用的调度例程[ **IoMarkIrpPending** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iomarkirppending)包括驱动程序将返回状态以外的值在其中至少一个路径\_PENDING。

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

 

 





