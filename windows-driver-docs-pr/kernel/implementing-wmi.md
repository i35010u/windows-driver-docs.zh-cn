---
title: 实现 WMI
description: 实现 WMI
ms.assetid: 5c2ed322-0fc9-4004-9a5f-f4d3c6a59fe9
keywords:
- WMI WDK 内核
- Windows Management Instrumentation WDK 内核
- 扩展 WDK WMI
- 测量数据 WDK WMI
- 检测数据 WDK WMI
- 用户模式下 WMI WDK
- WMI WDK 用户模式
- Windows Management Instrumentation WDK 用户模式
- 内核模式驱动程序 WDK WMI
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce8a27f9a1ae6b1f9aae042b76807355e01017a5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562746"
---
# <a name="implementing-wmi"></a>实现 WMI





本部分介绍 WDM 内核模式 Windows Management Instrumentation (WMI) 的扩展。 当将这些扩展添加到内核模式驱动程序时，您的驱动程序将成为 WMI 提供程序。 WMI 提供程序使度量和检测数据可供 WMI 使用者，如用户模式应用程序。

有关用户模式下 WMI API 的详细信息，请参阅[Windows Management Instrumentation](https://msdn.microsoft.com/library/aa394582(VS.85).aspx) Windows SDK 中。

如果要实现基于 KMDF 驱动程序，请参阅[中基于框架的驱动程序支持 WMI](https://msdn.microsoft.com/library/windows/hardware/ff544711)。

本部分包括有关内核模式 WMI 的以下信息：

[WMI 简介](introduction-to-wmi.md)

[WMI 体系结构](wmi-architecture.md)

[WMI 要求用于 WDM 驱动程序](wmi-requirements-for-wdm-drivers.md)

[WMI 数据和事件块的 MOF 语法](mof-syntax-for-wmi-data-and-event-blocks.md)

[设计 WMI 数据和事件块](designing-wmi-data-and-event-blocks.md)

[发布 WMI 架构](publishing-a-wmi-schema.md)

[注册为 WMI 数据提供程序](registering-as-a-wmi-data-provider.md)

[处理 WMI 请求](handling-wmi-requests.md)

[发送的 WMI 事件](sending-wmi-events.md)

[WMI 属性表](wmi-property-sheets.md)

[使用 wmimofck.exe](using-wmimofck-exe.md)

[WMI 事件跟踪](wmi-event-tracing.md)

[测试和故障排除 WMI 驱动程序支持](testing-and-troubleshooting-wmi-driver-support.md)

 

 




