---
title: Windows 2000 显示驱动程序模型 (XDDM) 路线图
description: 开发用于 Windows 2000 显示器驱动程序模型 (XDDM) 驱动程序的路线图
ms.assetid: 5f34d0ad-ab31-4361-9a42-83930aef267b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 12bd50b5d5318016e0e8581a10b0c7390cd410a2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566583"
---
# <a name="roadmap-for-the-windows-2000-display-driver-model-xddm"></a>Windows 2000 显示驱动程序模型 (XDDM) 路线图


![示意图，带有文本"wdk"上一条高速公路上叠加的路线图](images/wdkroadmap-th.png)Windows 2000 显示器驱动程序模型 (XDDM) 都需要图形硬件供应商提供的配对的显示器驱动程序和视频的微型端口驱动程序。 这两个显示这些驱动程序在内核模式下运行。

**请注意**  XDDM 和 VGA 驱动程序不会在 Windows 8 和更高版本上进行编译。 如果显示硬件附加到 Windows 8 计算机而无需经认证可支持 Windows 显示驱动程序模型 (WDDM) 1.2 或更高版本的驱动程序，则系统会默认到正在运行的 Microsoft 基本显示驱动程序。

 

若要在 Windows 7 和早期版本的 Windows 上创建 XDDM 显示器驱动程序，下载并安装 Windows 7 Windows Driver Kit (WDK) （内部版本 7600），请打开的 WDK 帮助文档**启动**菜单中，并遵循了建议主题中的步骤[开发驱动程序的 Windows 显示器驱动程序模型 (WDDM) 的路线图](roadmap-for-developing-drivers-for-the-windows-vista-display-driver-mo.md)。

 

 





