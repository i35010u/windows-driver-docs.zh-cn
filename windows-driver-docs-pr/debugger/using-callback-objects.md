---
title: 使用回调对象
description: 使用回调对象
ms.assetid: 9090a465-b6ab-4e99-8155-b0abdb729468
keywords:
- 调试器引擎 API，回调对象
- 回调对象
- 回调对象，事件回调
- 事件回调
- 回调对象，输入回调
- 输入回调
- 回调对象，输出回调
- 输出回调
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: b1e2b0cbc0be9f6da6a8eac9d9e0cbda1ec2dee7
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215684"
---
# <a name="using-callback-objects"></a>使用回调对象


有三个回调 COM，如引擎所使用的接口： [IDebugEventCallbacks](/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugeventcallbacks) ，用于通知 [调试器扩展](debugger-extensions.md) 和应用程序更改引擎或目标、 [IDebugInputCallbacks](/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebuginputcallbacks) 用于请求输入，以及用于发送输出的 [IDebugOutputCallbacks](/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugoutputcallbacks) 。

向客户端注册回调对象。 最多可以向每个客户端注册这三个回调接口中的每个实例， (接口计数的 Unicode 和 ASCII 版本作为相同的接口) 。

创建客户端时，引擎会记住在其中创建它的线程。 每当调用向客户端注册的回调实例时，引擎都将使用此同一个线程。 如果线程正在使用中，引擎将排队它需要进行的调用。 若要允许引擎进行这些调用，应在客户端的线程处于空闲状态时调用 [*DispatchCallbacks*](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-dispatchcallbacks) 方法。 方法 [**ExitDispatch**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-exitdispatch) 将导致 *DispatchCallbacks* 返回。 如果该线程是用于启动调试器会话的同一线程，则该引擎可以在 [**WaitForEvent**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-waitforevent) 方法中进行回调调用，而不需要调用 *DispatchCallbacks* 。

方法 [**FlushCallbacks**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-flushcallbacks) 告知引擎将所有缓冲的输出发送到输出回调。

### <a name="span-idevent_callbacksspanspan-idevent_callbacksspanevent-callback-objects"></a><span id="event_callbacks"></span><span id="EVENT_CALLBACKS"></span>事件回调对象

[IDebugEventCallbacks](/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugeventcallbacks)接口由引擎用来通知调试器扩展以及[事件](events.md#events)的应用程序和目标的更改。 可以使用[*SetEventCallbacks*](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-seteventcallbacks)将**IDebugEventCallbacks**的实现注册到客户端。 使用 [*GetEventCallbacks*](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-geteventcallbacks)可以找到向客户端注册的当前实现。 使用 [*GetNumberEventCallbacks*](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-getnumbereventcallbacks)可以找到在所有客户端上注册的事件回调的数目。

有关引擎如何管理事件的详细信息，请参阅 [监视事件](monitoring-events.md)。

### <a name="span-idinput_callbacksspanspan-idinput_callbacksspaninput-callback-objects"></a><span id="input_callbacks"></span><span id="INPUT_CALLBACKS"></span>输入回调对象

引擎使用 [IDebugInputCallbacks](/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebuginputcallbacks) 接口来请求调试器扩展和应用程序中的输入。 可以使用[*SetInputCallbacks*](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-setinputcallbacks)将**IDebugInputCallbacks**的实现注册到客户端。 使用 [*GetInputCallbacks*](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-getinputcallbacks)可以找到向客户端注册的当前实现。 使用 [*GetNumberInputCallbacks*](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-getnumberinputcallbacks)可以找到在所有客户端上注册的输入回调的数目。

有关引擎如何管理输入的详细信息，请参阅 [输入和输出](using-input-and-output.md)。

### <a name="span-idoutput_callbacksspanspan-idoutput_callbacksspanoutput-callback-objects"></a><span id="output_callbacks"></span><span id="OUTPUT_CALLBACKS"></span>输出回调对象

**IDebugOutputCallbacks**接口由引擎用来将输出发送到调试器扩展和应用程序。 可以使用[*SetOutputCallbacks*](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-setoutputcallbacks)将**IDebugOutputCallbacks**的实现注册到客户端。 使用 [*GetOutputCallbacks*](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-getoutputcallbacks)可以找到向客户端注册的当前实现。 使用 [*GetNumberOutputCallbacks*](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-getnumberoutputcallbacks)可以找到在所有客户端上注册的输出回调的数目。

有关引擎如何管理输出的详细信息，请参阅 [输入和输出](using-input-and-output.md)。

**注意**   与 COM 对象的典型一样，在向客户端注册时，引擎将在回调 COM 对象上调用**IUnknown：： AddRef** ，并且在对象被替换或删除客户端时， **Iunknown：： Release** 。

 

 

