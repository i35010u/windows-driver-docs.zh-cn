---
title: 报告图形内存
description: 报告图形内存
ms.assetid: a8a3dc08-1863-47ac-b41e-58ef38739c42
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fdd097bd4d790fca517556d041a6bab2ac39d376
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523817"
---
# <a name="reporting-graphics-memory"></a>报告图形内存


视频内存管理器向客户端报告显示微型端口驱动程序提供的内存信息。

Windows Vista 之前的操作系统报告图形内存为通过控制面板的单个数字**显示**应用程序。 显示器驱动程序提供给系统; 此数字操作系统然后通过向用户报告数**显示**应用程序。

视频内存管理器的[Windows 显示器驱动程序模型 (WDDM)](windows-vista-display-driver-model-design-guide.md)报告每个图形内存参与者的正确帐户。 以下客户端使用此报表：

-   Windows 系统评估工具 (WinSAT) 检查可用的图形内存，并采取措施以将关闭或打开基于可用内存量的高级 Aero Glass 体验。

-   桌面窗口管理器 (DWM) (Dwm.exe) 取决于可用的图形内存的计算机上的准确状态[Windows 显示驱动程序模型 (WDDM)](windows-vista-display-driver-model-design-guide.md)显示驱动程序。

-   Microsoft DirectX 游戏和其他图形应用程序必须能够获取准确描述的图形内存状态的值。 不准确的图形内存数量可能会显著更改用户的游戏体验。

以下部分描述的视频内存管理器如何计算图形内存数字，并提供如何报告内存号的示例：

[计算图形内存](calculating-graphics-memory.md)

[示例图形内存报告](examples-of-graphics-memory-reporting.md)

[检索图形内存数字](retrieving-graphics-memory-numbers.md)

 

 





