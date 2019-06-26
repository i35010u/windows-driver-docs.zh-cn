---
title: 使用回调对象
description: 使用回调对象
ms.assetid: 9090a465-b6ab-4e99-8155-b0abdb729468
keywords:
- 调试器引擎 API，回调对象
- 回调对象
- 回调对象，事件的回调
- 事件的回调
- 回调对象，输入回调
- 输入的回调
- 回调对象，输出回调
- 输出回调
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 18c293fff01458b000002857bececceca2e62e8f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368630"
---
# <a name="using-callback-objects"></a>使用回调对象


有三个回调 COM 等引擎使用的接口：[IDebugEventCallbacks](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nn-dbgeng-idebugeventcallbacks)通知[调试器扩展](debugger-extensions.md)和应用程序的更改到引擎或目标[IDebugInputCallbacks](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nn-dbgeng-idebuginputcallbacks)请求输入和[IDebugOutputCallbacks](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nn-dbgeng-idebugoutputcallbacks)发送输出。

与客户端注册回调对象。 最多可以向每个客户端 （Unicode 和 ASCII 的版本相同的接口作为接口计数） 注册的每三个回调接口的一个实例。

创建客户端时，引擎会记住在其中创建的线程。 每当对客户端中注册的回调实例在调用时，则引擎将使用同一个线程。 如果线程正在使用中，该引擎将排队等待它需要进行的调用。 若要使引擎可以使这些调用，该方法[ *DispatchCallbacks* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-dispatchcallbacks)每当客户端的线程处于空闲状态时，应调用。 该方法[ **ExitDispatch** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-exitdispatch)将导致*DispatchCallbacks*返回。 如果线程是用于启动调试器会话中，同一个线程，则引擎可以进行回调调用期间[ **WaitForEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-waitforevent)方法，和*DispatchCallbacks*不需要调用。

该方法[ **FlushCallbacks** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-flushcallbacks)可以使引擎以将所有缓冲的输出发送到输出回调。

### <a name="span-ideventcallbacksspanspan-ideventcallbacksspanevent-callback-objects"></a><span id="event_callbacks"></span><span id="EVENT_CALLBACKS"></span>事件的回调对象

[IDebugEventCallbacks](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nn-dbgeng-idebugeventcallbacks)引擎使用接口来通知调试器扩展和应用程序[事件](events.md#events)和引擎及其目标发生更改。 实现**IDebugEventCallbacks**可以注册使用的客户端[ *SetEventCallbacks*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-seteventcallbacks)。 可以使用查找注册到客户端的当前实现[ *GetEventCallbacks*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-geteventcallbacks)。 可以使用找到的事件的回调注册跨所有客户端数[ *GetNumberEventCallbacks*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-getnumbereventcallbacks)。

有关引擎如何管理事件的详细信息，请参阅[监视事件](monitoring-events.md)。

### <a name="span-idinputcallbacksspanspan-idinputcallbacksspaninput-callback-objects"></a><span id="input_callbacks"></span><span id="INPUT_CALLBACKS"></span>输入的回调对象

[IDebugInputCallbacks](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nn-dbgeng-idebuginputcallbacks)引擎使用接口来请求来自调试器扩展和应用程序的输入。 实现**IDebugInputCallbacks**可以注册使用的客户端[ *SetInputCallbacks*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-setinputcallbacks)。 可以使用查找注册到客户端的当前实现[ *GetInputCallbacks*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-getinputcallbacks)。 可以使用查找输入跨所有客户端注册的回调数目[ *GetNumberInputCallbacks*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-getnumberinputcallbacks)。

有关引擎如何管理输入的详细信息，请参阅[输入和输出](using-input-and-output.md)。

### <a name="span-idoutputcallbacksspanspan-idoutputcallbacksspanoutput-callback-objects"></a><span id="output_callbacks"></span><span id="OUTPUT_CALLBACKS"></span>输出回调对象

**IDebugOutputCallbacks**引擎使用接口来将输出发送到调试器扩展和应用程序。 实现**IDebugOutputCallbacks**可以注册使用的客户端[ *SetOutputCallbacks*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-setoutputcallbacks)。 可以使用查找注册到客户端的当前实现[ *GetOutputCallbacks*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-getoutputcallbacks)。 可以使用找到的输出回调注册跨所有客户端数量[ *GetNumberOutputCallbacks*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-getnumberoutputcallbacks)。

有关引擎如何管理输出的详细信息，请参阅[输入和输出](using-input-and-output.md)。

**请注意**  是典型的 COM 对象，该引擎将调用**iunknown:: Addref**回调 COM 对象时注册，通过客户端上并**iunknown:: Release**时对象被替换或删除客户端。

 

 

 





