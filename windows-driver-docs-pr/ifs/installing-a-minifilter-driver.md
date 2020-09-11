---
title: 安装筛选器驱动程序
description: 描述如何安装筛选器驱动程序
ms.assetid: c31aa104-404e-43e3-9215-2671ae6b12c0
keywords:
- 文件系统筛选器驱动程序 WDK，安装
- 文件系统微筛选器驱动程序 WDK，安装
- 筛选器驱动程序 WDK，安装
- 微筛选器驱动程序 WDK，安装
ms.date: 08/27/2020
ms.localizationpriority: medium
ms.openlocfilehash: 4aef1c973eaafd91c622b6b56c2272fb7eae2437
ms.sourcegitcommit: 2dd8e4262c30e3f8570e35da7b9485139b216ac8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90027554"
---
# <a name="installing-a-filter-driver"></a>安装筛选器驱动程序

文件系统筛选器驱动程序开发人员使用 INF 文件来安装和升级驱动程序。 您可以单独使用 INF 文件，或将其与批处理文件或用户模式安装应用程序一起使用。

本节包括：

* [创建筛选器驱动程序的 INF 文件](creating-an-inf-file-for-a-minifilter-driver.md)
* [筛选器驱动程序的加载顺序组和高度](load-order-groups-and-altitudes-for-minifilter-drivers.md)
* [分配的等级](allocated-altitudes.md)
* [筛选器海拔请求](minifilter-altitude-request.md)
* [重新分析点标记请求](reparse-point-tag-request.md)
