---
title: 指定 NDIS 版本信息
description: 指定 NDIS 版本信息
keywords:
- NDIS 版本信息 WDK
- 版本 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ef27573b92ae7763b398e19908c5a80970bc6945
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816531"
---
# <a name="specifying-ndis-version-information"></a>指定 NDIS 版本信息





本部分概述了 NDIS 和 NDIS 驱动程序为 NDIS 版本信息提供的支持。

许多 NDIS 结构在 **标头** 成员中包含结构版本信息。 NDIS 或 NDIS 驱动程序设置此类结构中的版本信息。 NDIS 驱动程序应该先在结构中检查版本信息，然后再访问结构成员。

此外，NDIS 驱动程序会在驱动程序初始化期间指定它们支持的 NDIS 版本。

本节包括下列主题：

-   [标头版本的 NDIS 支持概述](overview-of-ndis-support-for-header-versions.md)
-   [NDIS 驱动程序的版本信息要求](version-information-requirements-for-ndis-drivers.md)
-   [NDIS 的版本信息要求](version-information-requirements-for-ndis.md)
-   [获取 NDIS 版本](obtaining-the-ndis-version.md)
-   [WMI 的 NDIS 对象版本问题](ndis-object-version-issues-for-wmi.md)

## <a name="related-topics"></a>相关主题


[NDIS 版本概述](overview-of-ndis-versions.md)

 

 






