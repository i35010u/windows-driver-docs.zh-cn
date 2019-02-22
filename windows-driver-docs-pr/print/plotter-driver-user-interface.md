---
title: 绘图器驱动程序用户界面
description: 绘图器驱动程序用户界面
ms.assetid: 681e9215-d34b-4991-9c0f-b9dbe23412f6
keywords:
- 绘图器驱动程序 WDK 打印，用户界面
- MSPlot WDK 打印，用户界面
- 用户界面 WDK MSPlot
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 66298fc17c2c8253c447abbf075b05edbd4cedea
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555343"
---
# <a name="plotter-driver-user-interface"></a>绘图器驱动程序用户界面





绘图器用户界面采用[CPSUI](common-property-sheet-user-interface.md)创建以下两个属性表页：

-   **设备设置**打印机属性页中，当用户选择显示的页面**属性**从打印机文件夹或打印机窗口的菜单项。 此页列出了特定于打印机的配置设置。

-   **布局**，**纸张/质量**，并**高级**文档属性页中，当用户选择显示的页**文档默认值**菜单项从打印机文件夹或打印机窗口中，或当应用程序调用**PrinterProperties**或**DocumentProperties**函数 (中所述Microsoft Windows SDK 文档)。 此页列出了特定于文档的配置设置。

这些属性表包含绘图器功能和绘图仪的微型驱动程序指定选项。 它们还允许用户修改选项值。

作为用户模式下实现绘图仪的用户界面[打印机接口 DLL](printer-interface-dll.md)。 此 DLL，结合 CPSUI 中的代码指定了属性表页的内容。 DLL 执行的约束的绘图器选项可以组合，基于微型驱动程序中的信息。 此外可以确保用户未选择绘图器上未安装的选项。

 

 




