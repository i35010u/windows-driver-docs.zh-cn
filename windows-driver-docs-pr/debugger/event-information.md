---
title: 事件信息
description: 事件信息
ms.assetid: e6621b5d-f1af-4021-8832-43f79835a6c1
keywords:
- 目标事件
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 12f5b337cdbc368d49faead7ef92d2a92db39498
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361370"
---
# <a name="event-information"></a>事件信息


可访问调试会话时，没有*最后一个事件*。 这是导致会话变得可以访问的事件。 *事件目标*是生成的最后一个事件的目标。 当会话变为可访问时，当前的目标设置为事件目标。 返回的最后一个事件的详细信息[ **GetLastEventInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-getlasteventinformation)。 返回的最后一个事件并在指令指针在事件发生时的内存中的指令指针[**请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugadvanced3-request) operations [**调试\_请求\_获取\_CAPTURED\_事件\_代码\_偏移量**](https://docs.microsoft.com/windows-hardware/drivers/debugger/debug-request-get-captured-event-code-offset)并[**调试\_请求\_读取\_CAPTURED\_事件\_代码\_流**](https://docs.microsoft.com/windows-hardware/drivers/debugger/debug-request-read-captured-event-code-stream)。

如果目标是崩溃转储文件，*最后一个事件*是之前创建转储文件所做的最后一个事件。 转储文件中存储此事件，并在引擎它事件回调时生成转储文件获取作为调试目标。

如果目标是内核模式目标且*bug 检查*发生的错误检查代码和相关的参数可在使用[ **ReadBugCheckData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-readbugcheckdata)。

如果目标是用户模式下小型转储，转储文件生成器可以存储的其他事件。 通常情况下，这是导致生成器以保存转储文件的事件。 返回此事件的详细信息[ **GetStoredEventInformation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol4-getstoredeventinformation)并[**请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugadvanced3-request)操作[ **调试\_请求\_目标\_异常\_上下文**](https://docs.microsoft.com/windows-hardware/drivers/debugger/debug-request-target-exception-context)， [**调试\_请求\_目标\_异常\_线程**](https://docs.microsoft.com/windows-hardware/drivers/debugger/debug-request-target-exception-thread)，并[**调试\_请求\_目标\_异常\_记录**](https://docs.microsoft.com/windows-hardware/drivers/debugger/debug-request-target-exception-record).

转储文件可能包含事件的静态列表。 每个事件表示时间的特定点目标的快照。 返回此列表中的事件数[ **GetNumberEvents**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-getnumberevents)。 对于列表中的每个事件的说明，请使用[ **GetEventIndexDescription**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-geteventindexdescription)。 若要将事件设置为当前事件的此列表中，使用方法[ **SetNextEventIndex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-setnexteventindex); 在调用[ **WaitForEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-waitforevent)、事件将成为当前事件。 若要确定当前事件的事件列表中，使用[ **GetCurrentEventIndex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-getcurrenteventindex)。

 

 





