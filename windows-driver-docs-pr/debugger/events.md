---
title: Events
description: Events
ms.assetid: 2b086e78-ac4d-4f9c-a006-65f6f50b33f1
keywords:
- 调试器引擎，事件
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0be9ae2e40e695b29b29c4fb08f093aabd6edbbb
ms.sourcegitcommit: b316c97bafade8b76d5d3c30d48496915709a9df
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "79242816"
---
# <a name="events"></a>Events


## <span id="events"></span><span id="EVENTS"></span>


调试器引擎提供用于监视和响应目标中事件的工具。 当发生事件时，引擎将挂起目标（通常只是短暂），然后通知事件的所有客户端，进而指示引擎如何在目标中继续执行。

若要向客户端通知事件，引擎将调用已向客户端注册的事件回调对象。 引擎为每个事件回调提供事件的详细信息，事件回调指示引擎在目标中执行的执行方式。 当不同的事件回调提供了冲突的指令时，引擎将在具有最高优先级的指令上操作（请参阅[**调试\_状态\_XXX**](https://docs.microsoft.com/windows-hardware/drivers/debugger/debug-status-xxx)），这通常意味着选择涉及目标的最小执行的指令。

**请注意**   事件回调处理事件时，将挂起目标并访问调试会话;但是，因为引擎正在等待事件-无论是在[**WaitForEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-waitforevent)调用过程中显式执行，还是通过执行命令（如[**g （走）** ](g--go-.md)或[**p （Step））** ](p--step-.md)进行隐式调用，事件回调就无法调用**WaitForEvent**。如果尝试执行会导致调试器执行的任何命令，例如**g （转）** 或**p （步骤）** ，则引擎会将这些命令解释为如何继续操作的说明。

 

### <a name="span-idevent_filtersspanspan-idevent_filtersspanevent-filters"></a><span id="event_filters"></span><span id="EVENT_FILTERS"></span>事件筛选器

调试器引擎还提供*事件筛选器*，这是基本事件监视的更简单的替代方案。 事件筛选器提供一些简单的规则，这些规则指定是否应将事件打印到调试器的输出流或进入调试器。 它们还可用于在发生事件时执行调试器命令。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关监视事件的详细信息，请参阅[监视事件](monitoring-events.md)。

 

 





