---
title: 类型的筛选器驱动程序
description: 类型的筛选器驱动程序
ms.assetid: d3a92f10-5f5c-4640-ae03-1bf4e17c45ac
keywords:
- 筛选器驱动程序 WDK 网络类型
- NDIS 筛选器驱动程序 WDK，类型
- 修改筛选器驱动程序 WDK 网络
- 监视筛选器驱动程序 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 01b4d0f4da0394470a581c3cc164a951fbb306e2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520100"
---
# <a name="types-of-filter-drivers"></a>类型的筛选器驱动程序





有两种主要类型的筛选器驱动程序：

<a href="" id="monitoring"></a>监视  
这些筛选器驱动程序监视驱动程序堆栈中的行为。 但是，它们仅通过信息，而不修改驱动程序堆栈的行为。 监视筛选器驱动程序不能修改或来源的数据。

<a href="" id="modifying"></a>修改  
这些筛选器驱动程序修改驱动程序堆栈的行为。 修改的类型是特定于驱动程序。

**FilterType** INF 文件中的条目是用于监视筛选器驱动程序和用于修改筛选器驱动程序 0x00000002 0x00000001。

您可以指定筛选器驱动程序是必需的。 此功能通常用于修改筛选器驱动程序。 如果未加载必需的筛选器驱动程序，将销毁关联驱动程序堆栈。 有关必需的筛选器驱动程序的详细信息，请参阅[必需筛选器驱动程序](mandatory-filter-drivers.md)。

 

 





