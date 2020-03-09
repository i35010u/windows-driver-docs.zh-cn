---
title: 关于文件系统旧版筛选器驱动程序
description: 关于文件系统旧版筛选器驱动程序
ms.assetid: 8de28cd6-40be-48db-a839-335a85e48fc4
keywords:
- 旧筛选器驱动程序 WDK 文件系统，关于旧式文件系统筛选器驱动程序
- 文件系统旧筛选器驱动程序 WDK，关于文件系统旧筛选器驱动程序
- 什么是文件系统旧筛选器驱动程序
ms.date: 10/16/2019
ms.localizationpriority: medium
ms.openlocfilehash: f1265c5045dbb6259c53807a24c2e0bdef3376e1
ms.sourcegitcommit: 8c898615009705db7633649a51bef27a25d72b26
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/07/2020
ms.locfileid: "78910520"
---
# <a name="about-file-system-legacy-filter-drivers"></a>关于文件系统旧版筛选器驱动程序

本部分中的信息适用于正在维护现有旧筛选器驱动程序的开发人员。 旧文件系统筛选器模型已被[筛选器管理器和微筛选器驱动程序](https://docs.microsoft.com/windows-hardware/drivers/ifs/filter-manager-concepts)所取代。

> [!NOTE]
> 为了获得最佳的可靠性和性能，请使用带有筛选器管理器支持的[文件系统微筛选器驱动程序](https://docs.microsoft.com/windows-hardware/drivers/ifs/filter-manager-concepts)，而不是使用旧的文件系统 若要将旧驱动程序移植到微筛选器驱动程序，请参阅[迁移旧筛选器驱动程序的准则](guidelines-for-porting-legacy-filter-drivers.md)。
