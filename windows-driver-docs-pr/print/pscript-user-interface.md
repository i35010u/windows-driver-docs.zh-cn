---
title: Pscript 用户界面
description: Pscript 用户界面
ms.assetid: 88c1bb99-bc05-454f-ae36-722e9aa246c6
keywords:
- PostScript 打印机驱动程序 WDK 打印，用户界面
- Pscript WDK 打印，用户界面
- 用户界面 WDK Pscript
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 53c9a2026fcaae51e246fbe08d6a55538b45e280
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359016"
---
# <a name="pscript-user-interface"></a>Pscript 用户界面





Pscript 用户接口使用[CPSUI](common-property-sheet-user-interface.md)创建了以下属性表页：

-   **设备设置**打印机属性页中，当用户选择显示的页面**属性**从打印机文件夹或打印机窗口的菜单项。 页列出了特定于打印机的配置设置。

-   **布局**，**纸张/质量**，并**高级**文档属性页中，当用户选择显示的页**打印首选项**菜单项从打印机文件夹或打印机窗口中，或当应用程序调用**PrinterProperties**或**DocumentProperties**函数 (中所述Microsoft Windows SDK 文档)。 页面列出了特定于文档的配置设置。

这些属性表页包含打印机功能和指定的打印机的 Pscript 微型驱动程序的打印机选项。 它们还允许用户修改选项值。

作为用户模式下实现 Pscript 用户界面[打印机接口 DLL](printer-interface-dll.md)。 此 DLL，结合 CPSUI 中的代码指定了属性表页的内容。 DLL 强制实施的约束哪一台打印机选项可以组合，基于微型驱动程序中的信息。 此外可以确保用户未选择不安装在打印机上的选项。

可以通过提供修改 Pscript 提供属性表页[插件的用户界面](user-interface-plug-ins.md)，标题部分中所述[自定义 Microsoft 的打印机驱动程序](customizing-microsoft-s-printer-drivers.md)。

 

 




