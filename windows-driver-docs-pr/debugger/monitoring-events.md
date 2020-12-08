---
title: 监视事件
description: 监视事件
keywords:
- 调试器引擎，事件
- events
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8a209137b68b148bee5202ac17d557edb9ad5a3d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836869"
---
# <a name="monitoring-events"></a>监视事件


## <span id="ddk_monitoring_events_dbx"></span><span id="DDK_MONITORING_EVENTS_DBX"></span>


有关 [调试器引擎](introduction.md#debugger-engine)中事件的概述，请参阅 [事件](events.md)。

可使用 [IDebugEventCallbacks](/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugeventcallbacks) 接口监视目标或调试器引擎中发生的事件。 可以使用 [*SetEventCallbacks*](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-seteventcallbacks)将 **IDebugEventCallbacks** 对象注册到客户端。 每个客户端最多只能向其中注册一个 **IDebugEventCallbacks** 对象。

向客户端注册 **IDebugEventCallbacks** 对象时，引擎将调用该对象的 [**IDebugEventCallbacks：： GetInterestMask**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugeventcallbacks-getinterestmask) 来确定该对象感兴趣的事件。 只有对象感兴趣的事件才会发送到该对象。

对于每种类型的事件，引擎在 [IDebugEventCallbacks](/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugeventcallbacks)上调用相应的回叫方法。 对于来自目标的事件，从这些调用返回的 [**调试 \_ 状态 \_ XXX**](./debug-status-xxx.md) 值指定如何继续执行目标。 引擎从其调用的每个 **IDebugEventCallbacks** 对象中收集这些返回值，并对优先级最高的对象进行操作。

### <a name="span-idevents_from_the_target_that_break_into_the_debugger_by_defaultspanspan-idevents_from_the_target_that_break_into_the_debugger_by_defaultspanevents-from-the-target-that-break-into-the-debugger-by-default"></a><span id="events_from_the_target_that_break_into_the_debugger_by_default"></span><span id="EVENTS_FROM_THE_TARGET_THAT_BREAK_INTO_THE_DEBUGGER_BY_DEFAULT"></span>默认情况下中断到调试器的目标中的事件

默认情况下，下列事件会中断调试器：

-   断点事件

-   异常事件 (不记录在此处) 

-   系统错误

### <a name="span-idevents_from_the_target_that_do_not_break_into_the_debugger_by_defaultspanspan-idevents_from_the_target_that_do_not_break_into_the_debugger_by_defaultspanevents-from-the-target-that-do-not-break-into-the-debugger-by-default"></a><span id="events_from_the_target_that_do_not_break_into_the_debugger_by_default"></span><span id="EVENTS_FROM_THE_TARGET_THAT_DO_NOT_BREAK_INTO_THE_DEBUGGER_BY_DEFAULT"></span>默认情况下不会中断到调试器中的目标的事件

默认情况下，以下事件不会中断到调试器中：

-   创建进程事件

-   退出进程事件

-   创建线程事件

-   退出线程事件

-   加载模块事件

-   卸载模块事件

### <a name="span-idinternal_engine_changesspanspan-idinternal_engine_changesspaninternal-engine-changes"></a><span id="internal_engine_changes"></span><span id="INTERNAL_ENGINE_CHANGES"></span>内部引擎更改

以下不是实际事件，只是内部引擎更改：

-   目标更改

-   引擎更改

-   引擎符号更改

-   会话状态更改

 

