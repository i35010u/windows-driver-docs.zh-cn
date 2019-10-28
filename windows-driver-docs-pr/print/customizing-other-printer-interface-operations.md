---
title: 自定义其他打印机接口操作
description: 自定义其他打印机接口操作
ms.assetid: ae59d2e7-9049-432d-b519-9e7c88af8d48
keywords:
- 用户界面插件 WDK 打印，自定义方法
- UI 插件 WDK 打印，自定义方法
- IPrintOemUI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15d26537426a3787eb4b698dfd39625fe6e7f421
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843373"
---
# <a name="customizing-other-printer-interface-operations"></a>自定义其他打印机接口操作





UI 插件可以选择实现以下任何 IPrintOemUI 方法：

[**IPrintOemUI：:D eviceCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-devicecapabilities)

[**IPrintOemUI：:D evQueryPrintEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-devqueryprintex)

[**IPrintOemUI：:P rinterEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-printerevent)

[**IPrintOemUI::UpgradePrinter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-upgradeprinter)

方法等效于由 Unidrv 和 Pscript5 使用的用户模式[打印机接口 DLL](printer-interface-dll.md)导出的名称类似的函数。 这些自定义方法不会替换驱动程序的打印机接口 DLL 中的等效函数。 在每种情况下，首先调用打印机接口 DLL 函数，然后驱动程序调用插件的自定义方法。

 

 




