---
title: 绘图仪驱动程序功能
description: 绘图仪驱动程序功能
ms.assetid: 9fc32297-504c-453d-967b-ca4a4e56eaa2
keywords:
- 绘图器驱动程序 WDK 打印，功能
- MSPlot WDK 打印，功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d2a9abaedaa5c7fe1be8f51738aea9589de2656
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562590"
---
# <a name="plotter-driver-capabilities"></a>绘图仪驱动程序功能





Microsoft 绘图器驱动程序 (MSPlot) 提供了以下功能：

-   支持使用 HPGL/2 版本的 Hewlett-Packard 图形语言中，通过绘图器特定于模型的所有绘图[绘图器驱动程序微型驱动程序](plotter-driver-minidrivers.md)。

-   一个[绘图器驱动程序用户界面](plotter-driver-user-interface.md)根据树视图控件和属性表，对于所有绘图仪一致。

-   一个[绘图器驱动程序呈现器](plotter-driver-renderer.md)，GDI 图形引擎，以及 Win32 GDI 调用将从转换成可以发送到打印后台处理程序的打印机命令的应用程序。

若要为新 HPGL/2 合规的设备类型提供支持，您需要做是提供描述的设备的微型驱动程序。

 

 




