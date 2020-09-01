---
title: Windows Server 2008 和 Windows Vista SP1 的 WHEA 更改
description: Windows Server 2008 和 Windows Vista SP1 的 WHEA 更改
ms.assetid: fd66ee01-e262-45c2-bced-549192b0eca3
keywords:
- Windows 硬件错误体系结构 WDK，Windows Server 2008 更改
- Windows 硬件错误体系结构 WDK，Windows Vista SP1 更改
- WHEA WDK，Windows Server 2008 更改
- WHEA WDK，Windows Vista SP1 更改
- Windows Server 2008 WDK WHEA
- Windows Server 2008 WDK WHEA，WHEA 更改
- Windows Vista SP1 WDK WHEA
- Windows Vista SP1 WDK WHEA，WHEA 更改
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6df83f480ad9c4f697b34f17b774bd770eb9b8f3
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89209467"
---
# <a name="whea-changes-for-windows-server-2008-and-windows-vista-sp1"></a>Windows Server 2008 和 Windows Vista SP1 的 WHEA 更改


从 Windows Server 2008 和 Windows Vista SP1 开始，对 Windows 硬件错误体系结构进行了以下更改 (WHEA) ：

-   硬件平台供应商可以通过提供使用特定于平台的功能的 PSHED 插件来补充默认的 WHEA 平台特定硬件错误驱动程序 (PSHED) 功能。 PSHED 插件是一种专用的 Windows 设备驱动程序，可实现 PSHED 调用的回调接口。 PSHED 插件的用途是增加或覆盖 Microsoft 提供的 PSHED 的默认行为。

    有关 PSHED 插件的详细信息，请参阅 [特定于平台的硬件错误驱动程序插件](platform-specific-hardware-error-driver-plug-ins2.md)。

-   WHEA 支持错误记录永久性机制，允许将 [错误记录](error-records.md) 存储在非易失性存储中。 因此，如果由于出现严重硬件错误情况而必须重新启动操作系统，则会保留错误记录。 此机制将保留错误记录，以便重新启动系统时不会丢失任何与致命硬件错误条件相关的已捕获错误数据。

    有关错误记录持久性的详细信息，请参阅 [错误记录永久性机制](error-record-persistence-mechanism.md)。

-   每当发生硬件错误时，WHEA 将引发 Windows (ETW) 事件的事件跟踪。 从 Windows Server 2008 开始，WHEA 硬件错误事件和描述这些硬件错误事件的数据模板不同于 Windows Vista 上支持的事件和模板。

    有关 WHEA 内 ETW 支持的详细信息，请参阅 [硬件错误事件](/windows-hardware/drivers/ddi/_whea/)。

-   [WHEA 硬件错误事件处理应用程序](whea-hardware-error-event-processing-applications.md) 可以通过查询 WHEA 记录的任何事件，从系统事件日志中检索硬件错误事件。 但是，从 Windows Server 2008 开始，记录 WHEA 硬件错误事件的提供程序的名称已发生更改。 这些应用程序必须通过新提供程序访问错误事件。 有关详细信息，请参阅 [查询系统事件日志以获取硬件错误事件](querying-the-system-event-log-for-hardware-error-events.md)。

-   除了 WHEA 硬件错误事件处理应用程序以外，Windows Server 2008、Windows Vista SP1 和更高版本的 Windows 中现在还支持 [WHEA 管理应用程序](whea-management-applications.md) 。 通过 WHEA 提供的 WMI 接口，用户模式应用程序可以执行 WHEA 管理操作，例如启用或禁用错误源并注入硬件错误以供测试之用。

 

