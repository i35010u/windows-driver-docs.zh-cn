---
title: 绘图仪驱动程序用户界面
description: 绘图仪驱动程序用户界面
keywords:
- 绘图仪驱动程序 WDK 打印，用户界面
- MSPlot WDK 打印，用户界面
- 用户界面 WDK MSPlot
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c4e9f29a330ad4f56c3ec8569b8ed7e7da7f4523
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807589"
---
# <a name="plotter-driver-user-interface"></a>绘图仪驱动程序用户界面





绘图仪用户界面使用 [CPSUI](common-property-sheet-user-interface.md) 创建以下两个属性表页面：

-   打印机属性表的 " **设备设置** " 页，当用户从打印机文件夹或打印机窗口中选择 " **属性** " 菜单项时，将显示此页。 此页列出打印机特定的配置设置。

-   文档属性表的 " **布局**"、" **纸张/质量**" 和 " **高级** " 页，当用户选择 "打印机文件夹" 或 "打印机" 窗口中的 " **文档默认值** " 菜单项时，或者当应用程序调用 **PrinterProperties** 或 **DocumentProperties** 函数时，将在 Microsoft Windows SDK 文档) 中 (说明。 此页列出特定于文档的配置设置。

这些属性表包含绘图仪的微型驱动程序所指定的绘图仪功能和选项。 它们还允许用户修改选项值。

绘图仪的用户界面以用户模式 [打印机接口 DLL](printer-interface-dll.md)的形式实现。 此 DLL 中的代码与 CPSUI 结合，指定属性表页的内容。 根据微型驱动程序中的信息，DLL 强制实施可组合的绘图仪选项的约束。 它还确保用户不选择绘图仪上未安装的选项。

 

 




