---
title: 筛选器驱动程序的类型
description: 筛选器驱动程序的类型
keywords:
- 筛选器驱动程序 WDK 网络，类型
- NDIS 筛选器驱动程序 WDK，类型
- 修改筛选器驱动程序 WDK 网络
- 监视筛选器驱动程序 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9911ee9f5f14cda0cd708b1df7a4e08e78aced06
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815853"
---
# <a name="types-of-filter-drivers"></a>筛选器驱动程序的类型





筛选器驱动程序有两种主要类型：

<a href="" id="monitoring"></a>监视  
这些筛选器驱动程序监视驱动程序堆栈中的行为。 但是，它们只传递信息，并且不修改驱动程序堆栈的行为。 监视筛选器驱动程序不能修改或产生数据。

<a href="" id="modifying"></a>正在修改  
这些筛选器驱动程序修改驱动程序堆栈的行为。 修改的类型特定于驱动程序。

INF 文件中的 **FilterType** 条目是0x00000001 用于监视筛选器驱动程序，而不是用于修改筛选器驱动程序的0x00000002。

可以指定筛选器驱动程序是必需的。 此功能通常用于修改筛选器驱动程序。 如果必需的筛选器驱动程序未加载，则关联的驱动程序堆栈将被破坏。 有关必需筛选器驱动程序的详细信息，请参阅 [强制筛选器驱动程序](mandatory-filter-drivers.md)。

 

 





