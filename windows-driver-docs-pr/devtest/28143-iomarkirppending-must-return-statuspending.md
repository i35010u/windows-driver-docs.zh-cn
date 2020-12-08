---
title: C28143
description: 警告 C28143 调用也的调度例程还必须返回 STATUS_PENDING。
keywords:
- 列出用于驱动程序的 WDK PREfast 的警告
- 为驱动程序列出的 WDK PREfast 的错误
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28143
ms.openlocfilehash: 8857221aa58939a22d39d3fbb8732baf8b5915a2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793201"
---
# <a name="c28143"></a>C28143


警告 C28143：调用也的调度例程还必须返回状态 " \_ 挂起"

调用 [**也**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending) 的调度例程包含至少一个路径，在该路径中，驱动程序返回的值不是 "挂起" 状态 \_ 。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>示例

下面的代码示例 elicits 此警告。

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

 

