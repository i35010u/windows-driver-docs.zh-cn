---
title: 监视事件
description: 监视事件
ms.assetid: f0381cf9-e568-4789-af08-69d8b2c3ecbf
keywords:
- 调试器引擎事件
- 事件
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 614907f4c965e2ea93109f9c7e835691e2bb2ead
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354786"
---
# <a name="monitoring-events"></a>监视事件


## <span id="ddk_monitoring_events_dbx"></span><span id="DDK_MONITORING_EVENTS_DBX"></span>


有关中的事件的概述[调试器引擎](introduction.md#debugger-engine)，请参阅[事件](events.md)。

可以使用监视目标或调试器引擎中发生的事件[IDebugEventCallbacks](https://msdn.microsoft.com/library/windows/hardware/ff550550)接口。 **IDebugEventCallbacks**可能与使用的客户端注册对象[ *SetEventCallbacks*](https://msdn.microsoft.com/library/windows/hardware/ff556671)。 每个客户端只能有一个最多**IDebugEventCallbacks**对象注册到它。

当**IDebugEventCallbacks**通过客户端注册对象，该引擎将调用对象的[ **IDebugEventCallbacks::GetInterestMask** ](https://msdn.microsoft.com/library/windows/hardware/ff550737)确定哪个该对象对感兴趣的事件。 只有在其中所关注的对象的事件将发送给它。

对于每种类型的事件，该引擎调用相应的回调方法上[IDebugEventCallbacks](https://msdn.microsoft.com/library/windows/hardware/ff550550)。 来自目标的事件[**调试\_状态\_XXX** ](https://msdn.microsoft.com/library/windows/hardware/ff541651)从这些调用返回的值指定的目标执行应如何继续。 引擎从每个收集这些返回值**IDebugEventCallbacks**对象调用，并将对具有最高优先级的一个。

### <a name="span-ideventsfromthetargetthatbreakintothedebuggerbydefaultspanspan-ideventsfromthetargetthatbreakintothedebuggerbydefaultspanevents-from-the-target-that-break-into-the-debugger-by-default"></a><span id="events_from_the_target_that_break_into_the_debugger_by_default"></span><span id="EVENTS_FROM_THE_TARGET_THAT_BREAK_INTO_THE_DEBUGGER_BY_DEFAULT"></span>在默认情况下调试器中中断目标事件

默认情况下，以下事件进入调试器：

-   断点事件

-   异常事件 （此处未记录）

-   系统错误

### <a name="span-ideventsfromthetargetthatdonotbreakintothedebuggerbydefaultspanspan-ideventsfromthetargetthatdonotbreakintothedebuggerbydefaultspanevents-from-the-target-that-do-not-break-into-the-debugger-by-default"></a><span id="events_from_the_target_that_do_not_break_into_the_debugger_by_default"></span><span id="EVENTS_FROM_THE_TARGET_THAT_DO_NOT_BREAK_INTO_THE_DEBUGGER_BY_DEFAULT"></span>默认情况下调试器不会中断从目标事件

以下事件不会中断到调试器默认情况下：

-   创建进程事件

-   退出进程事件

-   创建线程事件

-   退出线程事件

-   加载模块事件

-   卸载模块事件

### <a name="span-idinternalenginechangesspanspan-idinternalenginechangesspaninternal-engine-changes"></a><span id="internal_engine_changes"></span><span id="INTERNAL_ENGINE_CHANGES"></span>内部引擎更改

以下不是实际事件，但只是内部引擎进行一些更改：

-   将目标更改

-   引擎更改

-   引擎符号更改

-   会话状态更改

 

 





