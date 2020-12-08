---
title: Windows 2000 显示驱动程序模型 (XDDM) 路线图
description: '用于开发 Windows 2000 显示器驱动程序模型的驱动程序的路线图 (XDDM) '
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 837b23afefdcad95e2d608079ec6b586c519bb8e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838049"
---
# <a name="roadmap-for-the-windows-2000-display-driver-model-xddm"></a>Windows 2000 显示驱动程序模型 (XDDM) 路线图


![图，该图中的文本 "wdk" 叠加在高速公路上](images/wdkroadmap-th.png)Windows 2000 显示器驱动程序模型 (XDDM) 要求图形硬件供应商提供配对的显示驱动程序和视频微型端口驱动程序。 这两个用于显示的驱动程序在内核模式下运行。

**注意**  在 Windows 8 及更高版本上，XDDM 和 VGA 驱动程序将不会编译。 如果将显示硬件连接到 Windows 8 计算机，而没有已认证的驱动程序支持 Windows 显示驱动程序模型 (WDDM) 1.2 或更高版本，则系统默认为运行 Microsoft 基本显示器驱动程序。

 

若要在 Windows 7 和更早版本的 Windows 上创建 XDDM 显示驱动程序，请下载并安装 Windows 7 Windows 驱动程序工具包 (WDK)  (版本 7600) ，从 " **开始** " 菜单打开 wdk 帮助文档，然后按照主题中的 [开发 Windows 显示驱动程序的驱动程序的指南 (WDDM)](roadmap-for-developing-drivers-for-the-windows-vista-display-driver-mo.md)中的建议步骤操作。

 

 





