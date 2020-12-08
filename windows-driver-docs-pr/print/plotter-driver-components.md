---
title: 绘图仪驱动程序组件
description: 绘图仪驱动程序组件
keywords:
- 绘图仪驱动程序 WDK 打印，组件
- MSPlot WDK 打印，组件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 299789b0ad6bb18cf9d3edfbbd1ab30b24a21395
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807607"
---
# <a name="plotter-driver-components"></a>绘图仪驱动程序组件





MSPlot 组件由 Dll 和二进制数据文件组成，如下图所示。

![阐释 msplot 组件如何包含 dll 和二进制数据文件的关系图](images/msplot.png)

关系图中的组件包括：

<a href="" id="application"></a>**程序**  
为用户提供打印功能的用户应用程序。

<a href="" id="gdi32-dll"></a>**gdi32.dll**  
导出 Win32 GDI 函数的用户模式 DLL。

<a href="" id="kernel-mode-graphics-engine"></a>**内核模式图形引擎**  
用于实现 GDI 功能的基于 NT 的操作系统执行代码。

<a href="" id="minidrivers"></a>**微型驱动程序**  
MSPlot 微型驱动程序 ( pcd 文件) 。

<a href="" id="cached--pcd-file-data"></a>**Pcd 文件数据**  
微型驱动程序从 pcd 文件中读取的数据。

<a href="" id="plotui-dll"></a>**plotui.dll**  
[绘图仪驱动程序用户界面](plotter-driver-user-interface.md) DLL，为所有支持 MSPlot 的打印机提供通用的 UI 代码。

<a href="" id="compstui-dll"></a>**compstui.dll**  
[CPSUI](common-property-sheet-user-interface.md) 用于打印机的用户界面。

<a href="" id="plotter-dll"></a>**plotter.dll**  
[绘图仪驱动程序呈现](plotter-driver-renderer.md)器，呈现映像并将图像数据流发送到后台处理程序。

 

 




