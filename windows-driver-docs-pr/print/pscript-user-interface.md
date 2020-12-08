---
title: Pscript 用户界面
description: Pscript 用户界面
keywords:
- PostScript 打印机驱动程序 WDK 打印，用户界面
- Pscript WDK 打印，用户界面
- 用户界面 WDK Pscript
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 79b038a7ff0a4860a9dd6a57f97dd1f44acb73b9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807135"
---
# <a name="pscript-user-interface"></a>Pscript 用户界面





Pscript 用户界面使用 [CPSUI](common-property-sheet-user-interface.md) 创建以下属性页：

-   打印机属性表的 " **设备设置** " 页，当用户从打印机文件夹或打印机窗口中选择 " **属性** " 菜单项时，将显示此页。 此页列出打印机特定的配置设置。

-   文档属性表的 " **布局**"、" **纸张/质量**" 和 " **高级** " 页，当用户从 "打印机" 文件夹或 "打印机" 窗口中选择 " **打印首选项** " 菜单项时，或者当应用程序调用 **PrinterProperties** 或 **DocumentProperties** 函数时，将在 Microsoft Windows SDK 文档) 中 (说明。 页面列出文档特定的配置设置。

这些属性表页面包含打印机的 Pscript 微型驱动程序指定的打印机功能和打印机选项。 它们还允许用户修改选项值。

Pscript 用户界面以用户模式 [打印机接口 DLL](printer-interface-dll.md)的形式实现。 此 DLL 中的代码与 CPSUI 结合，指定属性表页的内容。 根据微型驱动程序中的信息，DLL 强制对可以组合的打印机选项进行约束。 它还确保用户不会选择打印机上未安装的选项。

可以通过提供 [用户界面插件](user-interface-plug-ins.md)来修改 Pscript 提供的属性表页，该插件在标题为 " [自定义 Microsoft 的打印机驱动程序](customizing-microsoft-s-printer-drivers.md)" 部分中进行了介绍。

 

 




