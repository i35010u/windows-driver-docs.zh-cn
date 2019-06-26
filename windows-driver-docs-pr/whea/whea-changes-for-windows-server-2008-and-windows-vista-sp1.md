---
title: Windows Server 2008 和 Windows Vista SP1 的 WHEA 更改
description: Windows Server 2008 和 Windows Vista SP1 的 WHEA 更改
ms.assetid: fd66ee01-e262-45c2-bced-549192b0eca3
keywords:
- Windows 硬件错误体系结构 WDK，Windows Server 2008 的更改
- Windows 硬件错误体系结构 WDK，Windows Vista SP1 的更改
- WHEA WDK，Windows Server 2008 的更改
- WHEA WDK，Windows Vista SP1 的更改
- Windows Server 2008 WDK WHEA
- Windows Server 2008 WDK WHEA，WHEA 更改
- Windows Vista SP1 WDK WHEA
- Windows Vista SP1 WDK WHEA，WHEA 更改
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e6481d9c693a7c51b0100bf1ce3d010247865689
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387139"
---
# <a name="whea-changes-for-windows-server-2008-and-windows-vista-sp1"></a>Windows Server 2008 和 Windows Vista SP1 的 WHEA 更改


从 Windows Server 2008 和 Windows Vista SP1 开始，以下进行了更改到 Windows 硬件错误体系结构 (WHEA):

-   硬件平台供应商可以通过提供 PSHED 插件使用特定于平台的功能的补充默认 WHEA 特定于平台的硬件错误驱动程序 (PSHED) 功能。 PSHED 插件是实现一个回调接口，由 PSHED 调用一个专用的 Windows 设备驱动程序。 PSHED 插件旨在增强或重写 PSHED 由 Microsoft 提供的默认行为。

    有关 PSHED 插件的详细信息，请参阅[特定于平台的硬件错误驱动程序插件](platform-specific-hardware-error-driver-plug-ins2.md)。

-   WHEA 支持允许的错误记录持久性机制[错误记录](error-records.md)要存储在非易失性存储中。 因此，如果操作系统必须重新启动，因为致命硬件错误条件，将保留错误记录。 此机制，以便重新启动系统后会丢失任何致命硬件错误条件与相关的捕获的错误数据保留的错误记录。

    有关错误记录持久性的详细信息，请参阅[错误记录持久性机制](error-record-persistence-mechanism.md)。

-   WHEA 引发一个事件跟踪 Windows (ETW) 事件，每当硬件错误发生时。 从 Windows Server 2008 开始，WHEA 硬件错误事件和数据模板用于描述这些硬件错误事件的有不同的事件和 Windows Vista 支持的模板。

    WHEA 中 ETW 支持的详细信息，请参阅[硬件错误事件](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_whea/)。

-   [WHEA 硬件错误事件处理应用程序](whea-hardware-error-event-processing-applications.md)可以通过查询 WHEA 未记录任何事件从系统事件日志检索硬件错误事件。 但是，从 Windows Server 2008 开始，记录 WHEA 硬件错误事件提供程序的名称已更改。 这些应用程序必须通过新的提供程序访问的错误事件。 有关详细信息，请参阅[查询硬件错误事件的系统事件日志](querying-the-system-event-log-for-hardware-error-events.md)。

-   除了 WHEA 硬件错误事件处理应用程序， [WHEA 管理应用程序](whea-management-applications.md)现在支持 Windows Server 2008、 Windows Vista SP1 和更高版本的 Windows 中。 通过 WMI 界面提供的 WHEA，用户模式应用程序可以执行 WHEA 管理操作，例如启用或禁用错误源以及将注入以进行测试的硬件错误。

 

 




