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
ms.openlocfilehash: 52d846f697fb05ad7d73e5aa0949be2b5d97d736
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372385"
---
# <a name="customizing-other-printer-interface-operations"></a>自定义其他打印机接口操作





（可选），UI 插件可以实现以下 IPrintOemUI 方法：

[**IPrintOemUI::DeviceCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemui-devicecapabilities)

[**IPrintOemUI::DevQueryPrintEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemui-devqueryprintex)

[**IPrintOemUI::PrinterEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemui-printerevent)

[**IPrintOemUI::UpgradePrinter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemui-upgradeprinter)

方法是等效于同样命名的函数导出由用户模式[打印机接口 DLL](printer-interface-dll.md)由 Unidrv 和 Pscript5。 这些自定义方法不会替代驱动程序的打印机接口 DLL 中的等效函数。 每种情况下，首先，调用 DLL 函数中的打印机接口，然后该驱动程序调用插件的自定义方法。

 

 




