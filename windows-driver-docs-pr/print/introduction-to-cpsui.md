---
title: CPSUI 简介
description: CPSUI 简介
keywords:
- 公共属性表用户界面 WDK 打印，关于 CPSUI
- CPSUI WDK 打印，关于 CPSUI
- 属性表页 WDK 打印，关于 CPSUI 与打印机驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 838139042577f2a5f92afddd41f23d7acc0a03a1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796683"
---
# <a name="introduction-to-cpsui"></a>CPSUI 简介





 (CPSUI) 的公共属性表用户界面是一种用户模式的动态链接库，使开发人员能够创建具有常见标准外观的属性表页。 用 CPSUI 创建的大多数页包含：

-   Treeview 窗口，其中每个树节点表示一个可选择的、用户可修改的页选项。

-   用于显示和选择与节点关联的参数值的每个树节点的上下文菜单。

上下文菜单项是使用一组预定义的 [CPSUI 支持的窗口控件](cpsui-supported-window-controls.md)创建的。 用户在 treeview 窗口中选择一个选项，然后使用上下文菜单为该选项选择所需的值。

尽管 CPSUI 设计为供任何应用程序使用，但其主要用途是基于 NT 的操作系统打印子系统。 因此，Windows 驱动程序工具包 (WDK) 文档重点介绍这种用法。

CPSUI 为打印机和打印文档提供预定义的属性表页。 CPSUI 提供的页面包含打印机的 " **设备设置** " 页，以及文档的 " **布局**"、" **纸张/质量**" 和 " **高级** " 页。 可以从打印文件夹的 " **打印机** " 菜单查看这些页面。

打印后台处理程序与 [打印机接口 dll](printer-interface-dll.md)结合使用，这些预定义的页面可为打印机和文档创建属性表。 有关打印后台处理程序、打印机接口 Dll 和 CPSUI 如何交互的信息，请参阅将 [CPSUI 与打印机驱动程序配合使用](using-cpsui-with-printer-drivers.md)。

为 Microsoft 的 *Unidrv* 和 *Pscript* 驱动程序创建的自定义用户界面代码还可以使用 CPSUI。 有关详细信息，请参阅 [用户界面插件](user-interface-plug-ins.md)。

 

 




