---
title: CPSUI 简介
description: CPSUI 简介
ms.assetid: 737c2dbf-1ce6-4f83-af94-265c948f3128
keywords:
- 常见属性页用户界面 WDK 打印，有关 CPSUI
- 打印有关 CPSUI CPSUI WDK
- 属性表页 WDK 打印有关 CPSUI 与打印机驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 69cd6fff7da2f4b3b8668b8e10199805a75e5dc0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544620"
---
# <a name="introduction-to-cpsui"></a>CPSUI 简介





常用属性页用户界面 (CPSUI) 是一个用户模式动态链接库，开发人员可创建具有常见的标准外观的属性表页。 使用 CPSUI 创建的大多数页面组成：

-   树视图窗口，与每个树节点代表一个可选择用户可修改的页选项。

-   每个树节点，用于显示和选择与节点关联的参数值的上下文菜单。

创建使用一组预定义的上下文菜单项[CPSUI 支持窗口控件](cpsui-supported-window-controls.md)。 用户在树视图窗口中，选择一个选项，然后选择所需的值使用上下文菜单选项。

虽然 CPSUI 旨在供任何应用程序，但是其主要用途是基于 NT 的操作系统打印子系统。 因此，Windows Driver Kit (WDK) 文档重点介绍这种用法。

CPSUI 打印机和打印文档提供预定义的属性表页。 CPSUI 提供页面组成**设备设置**页上的打印机和**布局**，**纸张/质量**，并**高级**页文档。 这些页可查看从打印文件夹**打印机**菜单。

打印后台处理程序，结合[打印机接口 Dll](printer-interface-dll.md)，使用这些预定义的页来创建属性表为打印机和文档。 有关如何打印后台处理程序、 打印机接口的 Dll 和 CPSUI 交互的信息，请参阅[与打印机驱动程序使用 CPSUI](using-cpsui-with-printer-drivers.md)。

自定义用户界面代码为 Microsoft 的创建*Unidrv*并*Pscript*驱动程序还可以使用 CPSUI。 有关详细信息，请参阅[用户界面插件](user-interface-plug-ins.md)。

 

 




