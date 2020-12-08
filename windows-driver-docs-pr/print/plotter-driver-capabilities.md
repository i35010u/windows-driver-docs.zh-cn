---
title: 绘图仪驱动程序功能
description: 绘图仪驱动程序功能
keywords:
- 绘图仪驱动程序 WDK 打印，功能
- MSPlot WDK 打印，功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 22e89ad635d723bcca6f68411f6f5f5f690a9c3c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807601"
---
# <a name="plotter-driver-capabilities"></a>绘图仪驱动程序功能





Microsoft 绘图仪驱动程序 (MSPlot) 提供以下功能：

-   支持使用 Hewlett-Packard 图形语言的 HPGL/2 版本的所有绘图仪，方法是绘图仪模型特定的 [绘图仪驱动程序微型驱动程序](plotter-driver-minidrivers.md)。

-   基于 TreeView 控件和属性表的 [绘图仪驱动程序用户界面](plotter-driver-user-interface.md)，对于所有绘图仪均一致。

-   [绘图仪驱动程序呈现](plotter-driver-renderer.md)器，与 GDI 图形引擎一起，将应用程序中的 Win32 GDI 调用转换为可发送到打印后台处理程序的打印机命令。

若要为新的 HPGL/2 兼容设备类型提供支持，只需提供描述设备的微型驱动程序。

 

 




