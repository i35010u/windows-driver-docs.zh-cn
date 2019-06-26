---
title: 错误源控件
description: 错误源控件
ms.assetid: f73d9006-a7e7-4a0d-9654-004f53286743
keywords:
- Windows 硬件错误体系结构 WDK、 错误源控件
- WHEA WDK、 错误源控件
- 硬件错误 WDK WHEA，错误源代码管理
- 错误 WDK WHEA，错误源代码管理
- 特定于平台的硬件错误驱动程序插件 WDK WHEA，错误源代码管理
- PSHED 插件 WDK WHEA 错误源代码管理
- 错误源控制 WDK WHEA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 18f73c9824a9ace3ae1e395cfb87a80615f64010
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386481"
---
# <a name="error-source-control"></a>错误源控件


PSHED 公开的接口允许 Windows 内核控制的每种硬件平台由实现错误源的操作系统。 错误的源代码管理操作包括：

-   启用或禁用错误源。

-   设置或清除错误源与关联掩码位。 这些掩码位启用或禁用错误源的特定行为。

-   与错误源关联的严重性位设置。 这些严重性位控制的特定硬件错误报告给操作系统的严重级别。

-   设置与错误源关联的阈值参数。

Windows 内核调用 PSHED WHEA 管理应用程序配置错误源控件请求的响应中的错误源。 PSHED 支持的标准错误源的 PSHED 发现错误的源代码管理操作。 如果参与实现插件 PSHED[错误源发现](error-source-discovery.md)和其他错误源到操作系统 PSHED 不支持，插件 PSHED 必须也参与错误源的报表若要支持这些其他错误源的错误源控制操作的控件。 PSHED 插件可以选择性地参与错误源控制来重写 PSHED 控制一个或多个标准错误源的方式。

有关如何实现插件参与 PSHED 错误源控件中的详细信息，请参阅[参与错误源控制](participating-in-error-source-control.md)。

用户模式下管理应用程序控制错误源通过调用[WHEA 管理 API](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_whea/)。 有关如何实现 WHEA 管理应用程序的详细信息，请参阅[WHEA 管理应用程序](whea-management-applications.md)。

 

 




