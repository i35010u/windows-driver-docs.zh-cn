---
title: Events
description: Events
ms.assetid: 2b086e78-ac4d-4f9c-a006-65f6f50b33f1
keywords:
- 调试器引擎事件
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 44745610a99e22cb31de4c644c1d80322c65b841
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366885"
---
# <a name="events"></a>Events


## <span id="events"></span><span id="EVENTS"></span>


调试器引擎提供用于监视和响应中目标的事件的工具。 事件发生时，该引擎将挂起目标 （通常只是暂时的），然后通知所有客户端的事件，又指示引擎如何应在目标中继续执行。

若要通知的事件的客户端，该引擎调用客户端中注册事件回调对象。 引擎提供了详细信息，以及该事件，每个事件回调和事件回调指示引擎在上的目标中应如何继续执行的。 当不同事件的回调提供了冲突的说明时，该引擎作用于指令具有最高优先级 (请参阅[**调试\_状态\_XXX**](https://docs.microsoft.com/windows-hardware/drivers/debugger/debug-status-xxx))，它通常意味着选择涉及到的目标的最少执行的指令。

**请注意**  虽然事件回调处理事件、 目标已暂停，调试会话是可访问; 但是，因为引擎等待的事件-显式期间[ **WaitForEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-waitforevent)调用或隐式执行命令如[ **g （转向）** ](g--go-.md)或者[ **p （步骤）** ](p--step-.md)-不能调用事件回调**WaitForEvent**，并且如果它尝试执行的任何命令都将导致调试程序执行，例如**g （转向）** 或**p （步骤）** ，引擎会将这些命令解释为如何继续执行上一条指令。

 

### <a name="span-ideventfiltersspanspan-ideventfiltersspanevent-filters"></a><span id="event_filters"></span><span id="EVENT_FILTERS"></span>事件筛选器

调试器引擎还提供了*事件筛选器*，这是更简单的替代方案的基本事件监视。 事件筛选器提供了几个简单规则，指定到调试器的输出流或中断到调试器是否应打印事件。 它们还可以用于在事件发生时执行的调试器命令。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关监视事件的详细信息，请参阅[监视事件](monitoring-events.md)。

 

 





