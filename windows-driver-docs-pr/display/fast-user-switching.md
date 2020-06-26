---
title: 快速用户切换
description: 快速用户切换
ms.assetid: 79e13d56-f71f-4a7d-9069-de4821d29d94
keywords:
- 显示驱动程序模型 WDK Windows 2000，快速用户切换
- Windows 2000 显示器驱动程序模型 WDK，快速用户切换
- 视频微型端口驱动程序 WDK Windows 2000，快速用户切换
- 快速用户切换 WDK Windows 2000 显示器
- 多个虚拟显示器驱动程序 WDK Windows 2000 显示
- 虚拟显示器驱动程序 WDK Windows 2000 显示
- 显示驱动程序 WDK Windows 2000，快速用户切换
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0e95c082c3fd1c1aa7215b5870212260bf3865c
ms.sourcegitcommit: df7d6565a4cd2659c46d5fd83ef04a1672c60dbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/26/2020
ms.locfileid: "85382726"
---
# <a name="fast-user-switching"></a>快速用户切换

快速用户切换允许将多个用户登录到同一台计算机。 特定用户的桌面和任何正在运行的应用程序将从该用户的登录会话保留到下一个会话。

快速用户切换的工作方式是允许同时运行多个虚拟显示器驱动程序，其中每个虚拟显示器驱动程序都与特定的 PDEV 相关联。 但是，视频微型端口驱动程序作为单个实例存在。 当某个虚拟显示驱动程序调用视频微型端口驱动程序回调时，如果该显示驱动程序实例不再是活动内核线程，则在显示驱动程序的上下文中，如果微型端口驱动程序尝试访问传入的内存地址，不幸将会出现严重的问题。 显示驱动程序/视频微型端口驱动程序体系结构的原则是：信息只在一个方向上流动：从显示驱动程序到视频微型端口驱动程序。
