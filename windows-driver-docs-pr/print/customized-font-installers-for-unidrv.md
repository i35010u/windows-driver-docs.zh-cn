---
title: 自定义的 Unidrv 字体安装程序
description: 自定义的 Unidrv 字体安装程序
ms.assetid: d753368d-b1c8-454e-a02b-131dc778e723
keywords:
- 打印机驱动程序自定义 WDK，安装组件
- 自定义打印机驱动程序 WDK，安装组件
- 安装自定义打印机驱动程序组件 WDK
- 字体安装程序 WDK Unidrv
- uff 文件
- UFF 文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 34e9e24e997f39fdbec3d0b2e195a57e91ff9cb6
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89214902"
---
# <a name="customized-font-installers-for-unidrv"></a>自定义的 Unidrv 字体安装程序





对于字体盒文件未描述的墨盒字体，要求供应商提供的字体安装软件。 必须使用 [Unidrv 字体格式文件](customized-font-management.md#ddk-unidrv-font-format-files-gg) 描述这些字体)  (. uff 文件。 创建 uff 文件是供应商提供的字体安装程序的责任。

供应商提供的字体安装程序还应为可下载的 *PCL* 软字体提供支持。

创建自定义字体安装程序的两种方法如下所示：

-   提供用户界面插件

    此插件必须实现以下 COM 接口方法：

    [**IPrintOemUI::FontInstallerDlgProc**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-fontinstallerdlgproc)

    [**IPrintOemUI::UpdateExternalFonts**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-updateexternalfonts)

-   提供单独的可执行文件

    在字体安装过程中，可执行文件必须通过调用 Windows SDK 文档) 中所述的 SetPrinterData (，并指定 "FontInstaller" 键的值，将其名称存储在注册表中。

Unidrv 使用以下算法查找字体安装程序：

1.  如果字体安装程序可执行文件的名称存储在注册表中，则 Unidrv 不允许系统管理员从打印机的属性表中选择字体安装操作。 相反，管理员必须运行提供的可执行文件。

2.  如果安装程序可执行文件不可用，则 Unidrv 会启用从打印机的属性表中选择字体安装操作。 Unidrv 确定是否已安装用户界面插件。 如果是这样，则会调用其字体安装方法。 如果尚未安装用户界面插件，或者其字体安装方法返回 E \_ NOTIMPL，则驱动程序将使用自己的故障安装程序。

 

