---
title: 事件信息
description: 事件信息
ms.assetid: e6621b5d-f1af-4021-8832-43f79835a6c1
keywords:
- 目标，事件
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: b053de7fc305ace42e37e2b8de3aa35cbe35d0de
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89213027"
---
# <a name="event-information"></a>事件信息


只要调试会话可访问，就会出现 *最后一个事件*。 这是导致会话变为可访问的事件。 *事件目标*是生成最后一个事件的目标。 当会话变为可访问时，当前目标设置为事件目标。 最后一个事件的详细信息由 [**GetLastEventInformation**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getlasteventinformation)返回。 事件发生时，最后一个事件的指令指针和指令指针处的内存由 [**请求**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugadvanced3-request) 操作 [**调试 \_ 请求 \_ 获取 \_ 捕获的 \_ 事件 \_ 代码 \_ 偏移量**](./debug-request-get-captured-event-code-offset.md) 和 [**调试 \_ 请求 \_ 读取 \_ 捕获的 \_ 事件 \_ 代码 \_ 流**](./debug-request-read-captured-event-code-stream.md)返回。

如果目标是故障转储文件，则 *最后一个事件* 是在创建转储文件之前发生的最后一个事件。 此事件存储在转储文件中，当转储文件作为调试目标获取时，引擎将为事件回调生成该事件。

如果目标是内核模式目标并且发生了 *bug 检查* ，则可以使用 [**ReadBugCheckData**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-readbugcheckdata)查找 bug 检查代码和相关参数。

如果目标是用户模式小型转储，则转储文件生成器可能会存储其他事件。 通常，这是导致生成器保存转储文件的事件。 此事件的详细信息由 [**GetStoredEventInformation**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol4-getstoredeventinformation) 和 [**请求**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugadvanced3-request) 操作 [**调试 \_ 请求 \_ 目标 \_ 异常 \_ 上下文**](./debug-request-target-exception-context.md)、 [**调试 \_ 请求 \_ 目标 \_ 异常 \_ 线程**](./debug-request-target-exception-thread.md)和 [**调试 \_ 请求 \_ 目标 \_ 异常 \_ 记录**](./debug-request-target-exception-record.md)返回。

转储文件可能包含事件的静态列表。 每个事件都表示特定时间点的目标的快照。 [**GetNumberEvents**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getnumberevents)返回此列表中的事件数。 有关列表中每个事件的说明，请使用 [**GetEventIndexDescription**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-geteventindexdescription)。 若要将此列表中的事件设置为当前事件，请使用方法 [**SetNextEventIndex**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-setnexteventindex);在调用 [**WaitForEvent**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-waitforevent)之后，该事件将成为当前事件。 若要确定列表中的哪个事件是当前事件，请使用 [**GetCurrentEventIndex**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getcurrenteventindex)。

 

