---
title: 绘图器驱动程序组件
description: 绘图器驱动程序组件
ms.assetid: 6a976956-c188-4d31-b176-e97e09e8cc0b
keywords:
- 绘图器驱动程序 WDK 打印，组件
- MSPlot WDK 打印，组件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca72ad8a69679f708a65dada9be031724c1de4eb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543366"
---
# <a name="plotter-driver-components"></a>绘图器驱动程序组件





MSPlot 组件中包含的 Dll 和二进制数据文件，如以下关系图中所示。

![说明如何 msplot 组件包括 dll 和二进制数据文件的关系图](images/msplot.png)

在关系图中的组件包括：

<a href="" id="application"></a>**Application**  
用户应用程序的用户提供打印功能。

<a href="" id="gdi32-dll"></a>**gdi32.dll**  
导出 Win32 GDI 函数的用户模式 DLL。

<a href="" id="kernel-mode-graphics-engine"></a>**内核模式图形引擎**  
实现 GDI 功能的基于 NT 的操作系统执行代码。

<a href="" id="minidrivers"></a>**微型驱动程序**  
MSPlot 微型驱动程序 （.pcd 文件）。

<a href="" id="cached--pcd-file-data"></a>**缓存的.pcd 文件数据**  
微型驱动程序从.pcd 文件中读取数据。

<a href="" id="plotui-dll"></a>**plotui.dll**  
[绘图器驱动程序用户界面](plotter-driver-user-interface.md)DLL，为所有 MSPlot 支持打印机提供的常见 UI 代码。

<a href="" id="compstui-dll"></a>**compstui.dll**  
[CPSUI](common-property-sheet-user-interface.md)打印机用户界面。

<a href="" id="plotter-dll"></a>**plotter.dll**  
[绘图器驱动程序呈现器](plotter-driver-renderer.md)，其呈现图像并将图像数据流发送到后台处理程序。

 

 




