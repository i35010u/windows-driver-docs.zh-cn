---
title: 跟踪提供程序
description: 跟踪提供程序
ms.assetid: 06fcb37b-6cc3-4e64-8f53-86634836c7bd
keywords:
- 跟踪提供程序 WDK
- Windows WDK 的事件跟踪，提供程序
- ETW WDK，提供程序
- 提供程序 WDK 软件跟踪
- 跟踪会话 WDK，提供程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1c7d977fcc01eabafa9336a1ff73629ad5e178bc
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89381911"
---
# <a name="trace-provider"></a>跟踪提供程序


## <span id="ddk_trace_provider_tools"></span><span id="DDK_TRACE_PROVIDER_TOOLS"></span>


*跟踪提供程序*是用户模式应用程序或内核模式驱动程序的组件，它使用 Windows 的事件跟踪 (ETW) 技术来生成跟踪消息或跟踪事件。 通常，跟踪事件和消息报告提供程序的分离操作。 读取事件记录有助于了解提供程序在实际操作条件中所执行的操作。

[跟踪会话](trace-session.md)可包含多个跟踪提供程序。 这对于实现多个提供程序组件的跟踪驱动程序或应用程序特别有用，并用于跟踪多个驱动程序或交互的应用程序。

若要启动具有多个跟踪提供程序的跟踪会话，你必须在 GUID ( guid 扩展中指定所需的所有提供程序的 [控件 guid](control-guid.md)) 或你提交给 [跟踪控制器](trace-controller.md)的控件文件。 提供程序生成的跟踪消息将 ( .etl) 文件中。

内核模式驱动程序或用户模式应用程序可以支持多个跟踪提供程序组件，甚至可以在单个源文件中使用。 此功能对于在驱动程序或应用程序中跟踪特定操作非常有用。 若要实现多个跟踪提供程序，必须在每个提供程序的[WPP \_ 控件 \_ guid](/previous-versions/windows/hardware/previsioning-framework/ff556186(v=vs.85))宏中使用不同的[控件 guid](control-guid.md) 。

同样，多个驱动程序或应用程序可以是单个跟踪提供程序的一部分并共享其资源。 此功能在跟踪相关的应用程序和驱动程序（例如端口和微型端口驱动程序）时很有用。 若要实现此功能，请 \_ \_ 为每个提供程序在 WPP 控件 guid 宏中指定相同的控件 guid。