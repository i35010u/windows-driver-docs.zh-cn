---
title: Unidrv 用户界面
description: Unidrv 用户界面
keywords:
- Unidrv，用户界面
- 用户界面 WDK Unidrv
- Unidrv WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5617e9f4315295c7acf1cc8578fabcdab0fefb2b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835475"
---
# <a name="unidrv-user-interface"></a>Unidrv 用户界面





Unidrv 用户界面使用 [CPSUI](common-property-sheet-user-interface.md) 创建以下属性页：

-   打印机属性表的 " **设备设置** " 页，当用户从打印机文件夹或打印机窗口中选择 " **属性** " 菜单项时，将显示此页。 此页列出打印机特定的配置设置。

-   文档属性表的 " **布局**"、" **纸张/质量**" 和 " **高级** " 页，当用户选择 "打印机文件夹" 或 "打印机" 窗口中的 " **文档默认值** " 菜单项时，或者当应用程序调用 **PrinterProperties** 或 **DocumentProperties** 函数时，将在 Microsoft Windows SDK 文档) 中 (说明。 页面列出文档特定的配置设置。

这些属性表页面包含打印机的 Unidrv 微型驱动程序指定的 [打印机功能](printer-features.md) 和 [打印机选项](printer-options.md) 。 它们还允许用户修改选项值。

Unidrv 用户界面以用户模式 [打印机接口 DLL](printer-interface-dll.md)的形式实现。 此 DLL 中的代码与 CPSUI 结合，指定属性表页的内容。 根据微型驱动程序中的信息，DLL 强制对可以组合的打印机选项进行约束。 它还确保用户不会选择打印机上未安装的选项。

可以通过提供 [用户界面插件](user-interface-plug-ins.md)来修改 Unidrv 提供的属性表页。

 

 




