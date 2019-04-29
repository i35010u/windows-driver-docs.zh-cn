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
ms.openlocfilehash: 02ff9f920b156b9f66374fe084502d78edd79313
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63371596"
---
# <a name="using-callback-objects"></a>使用回调对象


有三个回调 COM 等引擎使用的接口：[IDebugEventCallbacks](https://msdn.microsoft.com/library/windows/hardware/ff550550)通知[调试器扩展](debugger-extensions.md)和应用程序的更改到引擎或目标[IDebugInputCallbacks](https://msdn.microsoft.com/library/windows/hardware/ff550785)请求输入和[IDebugOutputCallbacks](https://msdn.microsoft.com/library/windows/hardware/ff550801)发送输出。

与客户端注册回调对象。 最多可以向每个客户端 （Unicode 和 ASCII 的版本相同的接口作为接口计数） 注册的每三个回调接口的一个实例。

创建客户端时，引擎会记住在其中创建的线程。 每当对客户端中注册的回调实例在调用时，则引擎将使用同一个线程。 如果线程正在使用中，该引擎将排队等待它需要进行的调用。 若要使引擎可以使这些调用，该方法[ *DispatchCallbacks* ](https://msdn.microsoft.com/library/windows/hardware/ff541970)每当客户端的线程处于空闲状态时，应调用。 该方法[ **ExitDispatch** ](https://msdn.microsoft.com/library/windows/hardware/ff543265)将导致*DispatchCallbacks*返回。 如果线程是用于启动调试器会话中，同一个线程，则引擎可以进行回调调用期间[ **WaitForEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff561229)方法，和*DispatchCallbacks*不需要调用。

该方法[ **FlushCallbacks** ](https://msdn.microsoft.com/library/windows/hardware/ff545475)可以使引擎以将所有缓冲的输出发送到输出回调。

### <a name="span-ideventcallbacksspanspan-ideventcallbacksspanevent-callback-objects"></a><span id="event_callbacks"></span><span id="EVENT_CALLBACKS"></span>事件的回调对象

[IDebugEventCallbacks](https://msdn.microsoft.com/library/windows/hardware/ff550550)引擎使用接口来通知调试器扩展和应用程序[事件](events.md#events)和引擎及其目标发生更改。 实现**IDebugEventCallbacks**可以注册使用的客户端[ *SetEventCallbacks*](https://msdn.microsoft.com/library/windows/hardware/ff556671)。 可以使用查找注册到客户端的当前实现[ *GetEventCallbacks*](https://msdn.microsoft.com/library/windows/hardware/ff546601)。 可以使用找到的事件的回调注册跨所有客户端数[ *GetNumberEventCallbacks*](https://msdn.microsoft.com/library/windows/hardware/ff547896)。

有关引擎如何管理事件的详细信息，请参阅[监视事件](monitoring-events.md)。

### <a name="span-idinputcallbacksspanspan-idinputcallbacksspaninput-callback-objects"></a><span id="input_callbacks"></span><span id="INPUT_CALLBACKS"></span>输入的回调对象

[IDebugInputCallbacks](https://msdn.microsoft.com/library/windows/hardware/ff550785)引擎使用接口来请求来自调试器扩展和应用程序的输入。 实现**IDebugInputCallbacks**可以注册使用的客户端[ *SetInputCallbacks*](https://msdn.microsoft.com/library/windows/hardware/ff556721)。 可以使用查找注册到客户端的当前实现[ *GetInputCallbacks*](https://msdn.microsoft.com/library/windows/hardware/ff546892)。 可以使用查找输入跨所有客户端注册的回调数目[ *GetNumberInputCallbacks*](https://msdn.microsoft.com/library/windows/hardware/ff547923)。

有关引擎如何管理输入的详细信息，请参阅[输入和输出](using-input-and-output.md)。

### <a name="span-idoutputcallbacksspanspan-idoutputcallbacksspanoutput-callback-objects"></a><span id="output_callbacks"></span><span id="OUTPUT_CALLBACKS"></span>输出回调对象

**IDebugOutputCallbacks**引擎使用接口来将输出发送到调试器扩展和应用程序。 实现**IDebugOutputCallbacks**可以注册使用的客户端[ *SetOutputCallbacks*](https://msdn.microsoft.com/library/windows/hardware/ff556751)。 可以使用查找注册到客户端的当前实现[ *GetOutputCallbacks*](https://msdn.microsoft.com/library/windows/hardware/ff548071)。 可以使用找到的输出回调注册跨所有客户端数量[ *GetNumberOutputCallbacks*](https://msdn.microsoft.com/library/windows/hardware/ff547931)。

有关引擎如何管理输出的详细信息，请参阅[输入和输出](using-input-and-output.md)。

**请注意**  是典型的 COM 对象，该引擎将调用**iunknown:: Addref**回调 COM 对象时注册，通过客户端上并**iunknown:: Release**时对象被替换或删除客户端。

 

 

 





