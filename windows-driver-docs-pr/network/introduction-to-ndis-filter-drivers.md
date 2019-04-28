---
title: NDIS 筛选器驱动程序简介
description: NDIS 筛选器驱动程序简介
ms.assetid: dcf9b992-4812-43d7-9170-1a565d8db8fb
keywords:
- 筛选器驱动程序 WDK 网络，有关筛选器驱动程序
- NDIS 筛选器驱动程序 WDK，有关筛选器驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8d883cdbfb42d31392cb651e440b872d15faaa10
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343636"
---
# <a name="introduction-to-ndis-filter-drivers"></a>NDIS 筛选器驱动程序简介





筛选器驱动程序提供对微型端口驱动程序筛选服务。 NDIS 驱动程序堆栈必须包括微型端口驱动程序和协议驱动程序，并选择性地包含筛选器驱动程序。 有关 NDIS 驱动程序和驱动程序堆栈的详细信息，请参阅[驱动程序堆栈管理](driver-stack-management.md)。

以下应用程序可能要求筛选器驱动程序：

-   数据筛选应用程序的安全性或其他目的。

-   监视和收集网络数据统计信息的应用程序。

以下主题提供了筛选器驱动程序的特征和服务的简介：

[筛选器驱动程序特征](filter-driver-characteristics.md)

[筛选器驱动程序服务](filter-driver-services.md)

[类型的筛选器驱动程序](types-of-filter-drivers.md)

[必需的筛选器驱动程序](mandatory-filter-drivers.md)

 

 





