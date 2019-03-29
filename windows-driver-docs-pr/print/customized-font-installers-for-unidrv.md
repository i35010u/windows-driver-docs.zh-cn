---
title: 自定义的 Unidrv 字体安装程序
description: 自定义的 Unidrv 字体安装程序
ms.assetid: d753368d-b1c8-454e-a02b-131dc778e723
keywords:
- 自定义 WDK、 安装组件的打印机驱动程序
- 自定义打印机驱动程序 WDK、 安装组件
- 安装自定义打印机驱动程序组件 WDK
- 字体安装程序 WDK Unidrv
- .uff 文件
- UFF 文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6585b976e3d75e61b56374c697fde86dba1169e9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569339"
---
# <a name="customized-font-installers-for-unidrv"></a>自定义的 Unidrv 字体安装程序





需要由字体插件文件未描述的插件字体供应商提供的字体安装软件。 必须使用描述这些字体[Unidrv 字体格式文件](customized-font-management.md#ddk-unidrv-font-format-files-gg)（.uff 文件）。 创建.uff 文件负责的供应商提供的字体安装程序。

供应商提供的字体安装程序还应提供对支持可下载*PCL*软字体。

若要创建自定义的字体安装程序的两种技术如下所示：

-   提供插件的用户界面

    此插件必须实现以下 COM 接口方法：

    [**IPrintOemUI::FontInstallerDlgProc**](https://msdn.microsoft.com/library/windows/hardware/ff554176)

    [**IPrintOemUI::UpdateExternalFonts**](https://msdn.microsoft.com/library/windows/hardware/ff554188)

-   提供一个单独的可执行文件

    字体在安装期间，可执行文件必须存储在其名称注册表中通过调用 SetPrinterData （Windows SDK 文档中所述），并指定"FontInstaller"键的值。

Unidrv 查找字体安装程序使用以下算法：

1.  如果字体安装程序可执行文件的名称存储在注册表中，Unidrv 不允许系统管理员联系，以从打印机的属性表中选择字体安装操作。 相反，管理员必须运行提供的可执行文件。

2.  如果安装程序可执行文件不可用，Unidrv 可选择从打印机的属性表中的字体安装操作。 Unidrv 确定是否安装了插件的用户界面。 如果是这样，调用其字体安装方法。 如果尚未安装插件的用户界面，或者其字体安装方法返回 E\_NOTIMPL，驱动程序使用自己的容错的安装程序。

 

 




