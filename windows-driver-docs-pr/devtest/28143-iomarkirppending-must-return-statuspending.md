---
title: C28143
description: 警告 C28143 调用也的调度例程还必须返回 STATUS_PENDING。
ms.assetid: 3b9e6c4f-73d1-4abc-9495-85bb56e2532b
keywords:
- 列出用于驱动程序的 WDK PREfast 的警告
- 为驱动程序列出的 WDK PREfast 的错误
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28143
ms.openlocfilehash: c4af3096a51668c5c7c0c5bc8cdd327226ad2d7b
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89382593"
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

 

