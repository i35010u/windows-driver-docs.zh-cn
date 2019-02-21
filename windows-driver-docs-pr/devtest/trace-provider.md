---
title: 跟踪提供程序
description: 跟踪提供程序
ms.assetid: 06fcb37b-6cc3-4e64-8f53-86634836c7bd
keywords:
- 跟踪提供程序 WDK
- 事件跟踪的 Windows WDK，提供程序
- ETW WDK，提供程序
- 提供程序 WDK 软件跟踪
- 跟踪会话 WDK，提供程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ecfb692e9858394b05b8691f2d58fab814d5d0b4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523425"
---
# <a name="trace-provider"></a>跟踪提供程序


## <span id="ddk_trace_provider_tools"></span><span id="DDK_TRACE_PROVIDER_TOOLS"></span>


一个*跟踪提供程序*是它使用事件跟踪 Windows (ETW) 技术来生成跟踪事件或跟踪消息的用户模式应用程序或内核模式驱动程序的组件。 通常情况下，跟踪事件和消息将报告提供程序的离散操作。 读取事件的记录，可帮助你了解该提供程序在实际操作情况中执行的操作。

一个[跟踪会话](trace-session.md)可以包含多个跟踪提供程序。 这是用于跟踪驱动程序或应用程序实现多个提供程序组件，以及跟踪多个驱动程序或交互的应用程序特别有用。

若要使用多个跟踪提供程序启动跟踪会话，必须指定[控制 Guid](control-guid.md)的所有所需的提供程序中的 GUID （.guid 扩展名） 或控制文件提交到[跟踪控制器](trace-controller.md). 提供程序生成的跟踪消息混杂事件跟踪日志 (.etl) 文件中。

内核模式驱动程序或用户模式应用程序可以支持多个跟踪提供程序组件，即使在单个源文件中。 此功能可用于跟踪在驱动程序或应用程序中的特定操作。 若要实现多个跟踪提供程序，您必须使用不同[控制 GUID](control-guid.md)中[WPP\_控制\_GUID](https://msdn.microsoft.com/library/windows/hardware/ff556186)宏为每个提供程序。

同样，多个驱动程序或应用程序可以是单个跟踪提供程序的一部分并共享其资源。 在跟踪过程相关的应用程序和驱动程序，如端口和微型端口驱动程序，此功能非常有用。 若要实现此功能，指定相同的控件的 GUID 在 WPP\_控制\_每个提供程序 GUID 宏。
