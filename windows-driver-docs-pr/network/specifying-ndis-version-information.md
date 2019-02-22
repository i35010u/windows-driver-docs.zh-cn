---
title: 指定 NDIS 版本信息
description: 指定 NDIS 版本信息
ms.assetid: 9d007046-01c5-4bf8-adda-b88b596945d6
keywords:
- NDIS 版本信息 WDK
- 版本控制 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d94e438ff72f56e4eecbeaa809bffb4b9c74867e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520173"
---
# <a name="specifying-ndis-version-information"></a>指定 NDIS 版本信息





本部分提供了支持的概述，NDIS 和 NDIS 驱动程序提供有关 NDIS 版本信息。

许多 NDIS 结构包含结构中的版本信息**标头**成员。 NDIS 或 NDIS 驱动程序设置此类结构中的版本信息。 NDIS 驱动程序应检查结构中的版本信息，然后访问结构成员。

此外，NDIS 驱动程序指定它们支持驱动程序初始化期间的 NDIS 版本。

本部分包括以下主题：

-   [标头版本的 NDIS 支持概述](overview-of-ndis-support-for-header-versions.md)
-   [NDIS 驱动程序的版本信息要求](version-information-requirements-for-ndis-drivers.md)
-   [Ndis 版本信息要求](version-information-requirements-for-ndis.md)
-   [获取 NDIS 版本](obtaining-the-ndis-version.md)
-   [WMI 的 NDIS 对象版本问题](ndis-object-version-issues-for-wmi.md)

## <a name="related-topics"></a>相关主题


[NDIS 版本的概述](overview-of-ndis-versions.md)

 

 






