---
title: 错误源控件
description: 错误源控件
ms.assetid: f73d9006-a7e7-4a0d-9654-004f53286743
keywords:
- Windows 硬件错误体系结构 WDK，错误源控制
- WHEA WDK，错误源控制
- 硬件错误 WDK WHEA，错误源控制
- 错误 WDK WHEA，错误源控制
- 平台特定硬件错误驱动程序插件 WDK WHEA，错误源控制
- PSHED 插件 WDK WHEA，错误源控制
- 错误源控制 WDK WHEA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 30eecc7296654d42fb7295896ddc8318467396df
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89206153"
---
# <a name="error-source-control"></a>错误源控件


PSHED 向操作系统公开一个接口，该接口允许 Windows 内核控制硬件平台实现的每个错误源。 错误源代码管理操作包括：

-   启用或禁用错误源。

-   设置或清除与错误源关联的掩码位。 这些掩码位启用或禁用错误源的特定行为。

-   设置与错误源关联的严重级别。 这些严重性位控制向操作系统报告特定硬件错误时的严重级别。

-   设置与错误源关联的阈值参数。

Windows 内核调用 PSHED 来配置错误源，以响应 WHEA 管理应用程序对错误源控制请求的响应。 PSHED 支持 PSHED 发现的标准错误源的错误源代码管理操作。 如果实现了参与 [错误源发现](error-source-discovery.md) 的 PSHED 插件，并向 PSHED 不支持的操作系统报告其他错误源，则 PSHED 插件还必须参与错误源控制，以支持这些其他错误源的错误源代码管理操作。 PSHED 插件还可以选择参与错误源控制，以替代 PSHED 控制一个或多个标准错误源的方式。

有关如何实现参与错误源代码管理的 PSHED 插件的详细信息，请参阅 [参与错误源控制](participating-in-error-source-control.md)。

用户模式管理应用程序通过调用 [WHEA 管理 API](/windows-hardware/drivers/ddi/_whea/)来控制错误源。 有关如何实现 WHEA 管理应用程序的详细信息，请参阅 [WHEA 管理应用程序](whea-management-applications.md)。

 

