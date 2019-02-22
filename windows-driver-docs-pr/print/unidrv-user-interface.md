---
title: Unidrv 用户界面
description: Unidrv 用户界面
ms.assetid: b1f34ebf-8c8a-4b43-ba48-26bcf6352360
keywords:
- Unidrv，用户界面
- 用户界面 WDK Unidrv
- Unidrv WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 80eac4b200fe578cd9e4a2a8214fe41096f04719
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543586"
---
# <a name="unidrv-user-interface"></a>Unidrv 用户界面





Unidrv 用户接口使用[CPSUI](common-property-sheet-user-interface.md)创建了以下属性表页：

-   **设备设置**打印机属性页中，当用户选择显示的页面**属性**从打印机文件夹或打印机窗口的菜单项。 页列出了特定于打印机的配置设置。

-   **布局**，**纸张/质量**，并**高级**文档属性页中，当用户选择显示的页**文档默认值**菜单项从打印机文件夹或打印机窗口中，或当应用程序调用**PrinterProperties**或**DocumentProperties**函数 (中所述Microsoft Windows SDK 文档)。 页面列出了特定于文档的配置设置。

这些属性表页包含[打印机功能](printer-features.md)并[打印机选项](printer-options.md)指定打印机的 Unidrv 微型驱动程序。 它们还允许用户修改选项值。

作为用户模式下实现 Unidrv 用户界面[打印机接口 DLL](printer-interface-dll.md)。 此 DLL，结合 CPSUI 中的代码指定了属性表页的内容。 DLL 强制实施的约束哪一台打印机选项可以组合，基于微型驱动程序中的信息。 此外可以确保用户未选择不安装在打印机上的选项。

可以通过提供修改 Unidrv 提供属性表页[插件的用户界面](user-interface-plug-ins.md)。

 

 




