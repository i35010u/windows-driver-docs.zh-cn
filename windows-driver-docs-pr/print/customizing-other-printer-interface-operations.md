---
title: 自定义其他打印机接口操作
description: 自定义其他打印机接口操作
keywords:
- 用户界面插件 WDK 打印，自定义方法
- UI 插件 WDK 打印，自定义方法
- IPrintOemUI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b83300d96172e451d6cc5d64753e6cf2e256629
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797371"
---
# <a name="customizing-other-printer-interface-operations"></a>自定义其他打印机接口操作





UI 插件可以选择实现以下任何 IPrintOemUI 方法：

[**IPrintOemUI：:D eviceCapabilities**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-devicecapabilities)

[**IPrintOemUI：:D evQueryPrintEx**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-devqueryprintex)

[**IPrintOemUI：:P rinterEvent**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-printerevent)

[**IPrintOemUI::UpgradePrinter**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-upgradeprinter)

方法等效于由 Unidrv 和 Pscript5 使用的用户模式 [打印机接口 DLL](printer-interface-dll.md) 导出的名称类似的函数。 这些自定义方法不会替换驱动程序的打印机接口 DLL 中的等效函数。 在每种情况下，首先调用打印机接口 DLL 函数，然后驱动程序调用插件的自定义方法。

 

