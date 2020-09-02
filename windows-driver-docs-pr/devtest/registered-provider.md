---
title: 已注册的提供程序
description: 已注册的提供程序
ms.assetid: d16e91d7-40ce-4a35-b3a7-f46f26a810bb
keywords:
- 已注册的提供程序 WDK 软件跟踪
- 跟踪提供程序 WDK
- Windows WDK 的事件跟踪，提供程序
- ETW WDK，提供程序
- 提供程序 WDK ETW
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4f9f53fbe7df7ee8b09eb13819061a2b16efe066
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89381915"
---
# <a name="registered-provider"></a>已注册的提供程序

## <span id="ddk_registered_provider_tools"></span><span id="DDK_REGISTERED_PROVIDER_TOOLS"></span>

*已注册的提供程序*是一个[跟踪提供程序](trace-provider.md)，它为[Windows (ETW) 注册事件跟踪](event-tracing-for-windows--etw-.md)。 用户可以枚举已注册的提供程序，并按名称引用它们。

跟踪提供程序必须在启动时注册 ETW，方法是调用 **EventRegister** ，或者通过使用 "注册宏" 或跟踪框架提供的函数（例如，wpp 提供的 [wpp \_ INIT \_ 跟踪](/previous-versions/windows/hardware/previsioning-framework/ff556191(v=vs.85)) 宏）来注册。 它们会在停止之前（通过调用 **EventUnregister** 或使用 framework 取消注册宏或函数）注销。 无法启用不注册自身的跟踪提供程序，也不会从中收集任何事件。

若要显示已注册的提供程序中的事件，请使用 [TraceView](traceview.md)。 有关说明，请参阅为 [注册的提供程序创建跟踪会话](creating-a-trace-session-for-a-registered-provider.md)。

有关已注册提供程序的详细信息，请参阅 Microsoft Windows SDK 中的 [事件跟踪](/windows/desktop/ETW/event-tracing-portal) 。