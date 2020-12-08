---
title: 报告图形内存
description: 报告图形内存
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d045d2ee122cc0dc2e31163694cd060a46cc7d4f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825701"
---
# <a name="reporting-graphics-memory"></a>报告图形内存


视频内存管理器向客户端报告显示微型端口驱动程序提供的内存信息。

Windows Vista 之前的操作系统通过控制面板 **显示** 应用程序将图形内存报告为单个数字。 显示驱动程序向操作系统提供此编号;然后，操作系统通过 **显示** 应用程序向用户报告数字。

[Windows 显示驱动程序模型 (WDDM) ](windows-vista-display-driver-model-design-guide.md)的视频内存管理器报告每个图形内存参与者的准确帐户。 以下客户端使用此报告：

-   Windows 系统评估工具 (WinSAT) 检查是否有可用的图形内存，并采取相应的措施关闭或打开基于可用内存量的高级 Aero 玻璃体验。

-    ( # A0) 的桌面窗口管理器 (DWM) 依赖于计算机上可用图形内存的确切状态， [ (WDDM) ](windows-vista-display-driver-model-design-guide.md) 显示驱动程序。

-   Microsoft DirectX 游戏和其他图形应用程序必须能够获取描述图形内存状态的准确值。 图形内存编号不准确可能会显著改变用户的游戏体验。

以下各节介绍视频内存管理器如何计算图形内存号，并提供有关如何报告内存号的示例：

[计算图形内存](calculating-graphics-memory.md)

[图形内存报告示例](examples-of-graphics-memory-reporting.md)

[检索图形内存数字](retrieving-graphics-memory-numbers.md)

 

 





