---
title: 关于文件系统旧版筛选器驱动程序
description: 关于文件系统旧版筛选器驱动程序
keywords:
- 旧筛选器驱动程序 WDK 文件系统，关于旧式文件系统筛选器驱动程序
- 文件系统旧筛选器驱动程序 WDK，关于文件系统旧筛选器驱动程序
- 什么是文件系统旧筛选器驱动程序
ms.date: 10/16/2019
ms.localizationpriority: medium
ms.openlocfilehash: f17914be4ef6e96f5ff9eef5b3bb29e19d298a54
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96791789"
---
# <a name="about-file-system-legacy-filter-drivers"></a>关于文件系统旧版筛选器驱动程序

本部分中的信息适用于正在维护现有旧筛选器驱动程序的开发人员。 旧文件系统筛选器模型已被 [筛选器管理器和微筛选器驱动程序](./filter-manager-concepts.md)所取代。

> [!NOTE]
> 为了获得最佳的可靠性和性能，请使用带有筛选器管理器支持的 [文件系统微筛选器驱动程序](./filter-manager-concepts.md) ，而不是使用旧的文件系统 若要将旧驱动程序移植到微筛选器驱动程序，请参阅 [迁移旧筛选器驱动程序的准则](guidelines-for-porting-legacy-filter-drivers.md)。
