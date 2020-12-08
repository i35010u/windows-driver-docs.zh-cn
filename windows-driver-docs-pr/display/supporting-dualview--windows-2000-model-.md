---
title: 支持 DualView（Windows 2000 模型）
description: 支持 DualView（Windows 2000 模型）
keywords:
- 视频微型端口驱动程序 WDK Windows 2000、双屏
- 双屏显示 WDK 视频微型端口
- 多个显示设备同时 WDK 视频微型端口
- SingleView WDK 视频微型端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7e533daaa33cf985b4f5fefa6a9dd965633a783c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789971"
---
# <a name="supporting-dualview-windows-2000-model"></a>支持 DualView（Windows 2000 模型）


许多新式显示适配器能够同时驱动两个或更多不同的显示设备。 Windows XP 和更高版本的一项功能，它为类似于 Multimonitor 的功能提供系统级支持，但只需要一个显示适配器。 对于双屏和 Multimonitor，图形设备接口 (GDIs) 和最终用户体验相同。

SingleView 模式

在 SingleView 模式下，显示适配器驱动单个显示设备，而不考虑监视器数量。 对于 Windows 2000 和更高版本的操作系统版本当前支持的大多数显示适配器，这是正常模式。

双屏模式

处于双屏模式的计算机可以使用包含多个视频端口的单个显示适配器 () 在不同监视器上驱动多个图像，每个显示设备描绘桌面的不同部分。 主映像显示 *主视图*;其他图像显示 *辅助视图*。

以下子节提供了有关双屏的详细信息：

[启用 DualView](enabling-dualview.md)

[DualView 高级实施详细信息](dualview-advanced-implementation-details.md)

 

 





