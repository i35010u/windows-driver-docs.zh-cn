---
title: 支持 DualView（Windows 2000 模型）
description: 支持 DualView（Windows 2000 模型）
ms.assetid: 08da97c9-1d31-40f5-99df-5f16eaa47c79
keywords:
- 微型端口驱动程序 WDK Windows 2000 中，双视图
- 双视图 WDK 微型端口
- 多个显示设备同时 WDK 视频微型端口
- SingleView WDK 微型端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2d90d09e2e0ed83cd554c1c932e21767d4da2c29
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372745"
---
# <a name="supporting-dualview-windows-2000-model"></a>支持 DualView（Windows 2000 模型）


许多现代显示适配器都能够同时驱动器两个或多个不同的显示设备。 双视图，一项功能的 Microsoft Windows XP 及更高版本，提供系统级别的支持功能的多显示器，类似，但要求只有单个显示屏适配器。 图形设备接口 (GDIs) 和最终用户体验是相同的双视图和多显示器。

SingleView 模式

在 SingleView 模式下，显示适配器驱动的单个显示屏设备，而不考虑监视器的数目。 这是 Windows 2000 和更高版本的操作系统版本当前支持的显示适配器的大部分的常用模式。

双视图模式

双视图模式中的计算机可以使用 （具有多个视频端口） 的单个显示屏适配器来驱动不同监视器上的多个映像，与饰演桌面的不同部分的每个显示设备。 主图像将显示*主视图*; 其他映像显示*辅助视图*。

以下各小节提供有关双视图的详细信息：

[启用双视图](enabling-dualview.md)

[双视图高级实现详细信息](dualview-advanced-implementation-details.md)

 

 





