---
title: 已注册的提供程序
description: 已注册的提供程序
ms.assetid: d16e91d7-40ce-4a35-b3a7-f46f26a810bb
keywords:
- 注册的提供程序 WDK 软件跟踪
- 跟踪提供程序 WDK
- 事件跟踪的 Windows WDK，提供程序
- ETW WDK，提供程序
- WDK ETW 提供程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c066c16fc7c8ccdfd940f86d8a95ec55b32f23fd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523963"
---
# <a name="registered-provider"></a>已注册的提供程序

## <span id="ddk_registered_provider_tools"></span><span id="DDK_REGISTERED_PROVIDER_TOOLS"></span>

一个*注册的提供程序*是[跟踪提供程序](trace-provider.md)注册[事件跟踪 Windows (ETW)](event-tracing-for-windows--etw-.md)。 用户可以枚举已注册的提供程序，并按名称引用它们。

跟踪提供程序必须向 ETW 注册，在启动时通过调用**EventRegister**或通过使用注册宏或函数提供的一种跟踪框架，如[WPP\_INIT\_跟踪](https://msdn.microsoft.com/library/windows/hardware/ff556191)WPP 所提供的宏。 只需才会停止，或者通过调用它们注销**EventUnregister**或通过使用框架注销宏或函数。 不能启用并不能注册的跟踪提供程序，并且将从其收集任何事件。

若要显示来自已注册的提供程序的事件，请使用[TraceView](traceview.md)。 有关说明，请参阅[为已注册的提供程序创建跟踪会话](creating-a-trace-session-for-a-registered-provider.md)。

有关注册的提供程序的详细信息，请参阅[事件跟踪](https://msdn.microsoft.com/library/windows/desktop/bb968803)Microsoft Windows SDK 中。
