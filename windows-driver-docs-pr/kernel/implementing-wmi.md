---
title: 实现 WMI
description: 实现 WMI
ms.assetid: 5c2ed322-0fc9-4004-9a5f-f4d3c6a59fe9
keywords:
- WMI WDK 内核
- Windows Management Instrumentation WDK 内核
- 扩展 WDK WMI
- 度量数据 WDK WMI
- 检测数据 WDK WMI
- 用户模式 WMI WDK
- WMI WDK 用户模式
- Windows Management Instrumentation WDK 用户模式
- 内核模式驱动程序 WDK、WMI
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8a42ca4a5bbdb27690ab7d7a68398f2ba847de60
ms.sourcegitcommit: 6c42efc074ab939e7737d6c2b016d3f3a75954e1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90741030"
---
# <a name="implementing-wmi"></a>实现 WMI





本部分介绍 (WMI) extension 到 WDM 的内核模式 Windows Management Instrumentation。 将这些扩展添加到内核模式驱动程序时，驱动程序将成为 WMI 提供程序。 WMI 提供程序使度量和检测数据可用于 WMI 使用者，如用户模式应用程序。

有关用户模式 WMI API 的详细信息，请参阅 Windows SDK 中的 [Windows Management Instrumentation](/windows/desktop/WmiSdk/wmi-start-page) 。

如果要实现基于 KMDF 的驱动程序，请参阅 [基于框架的驱动程序中的支持 WMI](../wdf/introduction-to-wmi-for-kmdf-drivers.md)。

本部分包括有关内核模式 WMI 的下列信息：

[WMI 简介](introduction-to-wmi.md)

[WMI 体系结构](wmi-architecture.md)

[WDM 驱动程序的 WMI 要求](wmi-requirements-for-wdm-drivers.md)

[WMI 数据和事件块的 MOF 语法](mof-syntax-for-wmi-data-and-event-blocks.md)

[设计 WMI 数据和事件块](designing-wmi-data-and-event-blocks.md)

[发布 WMI 架构](publishing-a-wmi-schema.md)

[注册为 WMI 数据提供程序](registering-as-a-wmi-data-provider.md)

[处理 WMI 请求](handling-wmi-requests.md)

[发送 WMI 事件](sending-wmi-events.md)

[WMI 属性表](wmi-property-sheets.md)

[使用 wmimofck.exe](using-wmimofck-exe.md)

[WMI 事件跟踪](wmi-event-tracing.md)

[测试 WMI 驱动程序支持及排查其问题](general-techniques-for-testing-wmi-driver-support.md)

