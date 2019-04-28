---
title: OpenPrinter
description: OpenPrinter
ms.assetid: 8bbb46a8-2bba-4d15-a2e2-4770b52d2505
keywords:
- OpenPrinter
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f1fca25391ddbc2f2906e787ae2f2b8617ab8fa5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339911"
---
# <a name="openprinter"></a>OpenPrinter


打开打印队列时 (通过使用`OpenPrinter`函数)，打印驱动程序加载和的以下方法[IPrintTicketProvider 接口](https://msdn.microsoft.com/library/windows/hardware/ff554375)调用顺序如下：

1.  [**IPrintTicketProvider::GetSupportedVersions**](https://msdn.microsoft.com/library/windows/hardware/ff554371)

2.  [**IPrintTicketProvider::BindPrinter**](https://msdn.microsoft.com/library/windows/hardware/ff554354)

3.  [**IPrintTicketProvider::QueryDeviceNamespace**](https://msdn.microsoft.com/library/windows/hardware/ff554378)

方法**IPrintTicketProvider** Unidrv 或 PScript5 打印驱动程序调用中的接口**IPrintOemPrintTicketProvider**驱动程序由托管的每个插件方法。 下图和列表显示如何这些调用时将执行`OpenPrinter`调用。

![说明调用序列 openprinter 的关系图](images/ptpcopen-uml.gif)

1.  每个插件，请调用[ **IPrintOemPrintTicketProvider::GetSupportedVersions**](https://msdn.microsoft.com/library/windows/hardware/ff553170)。

2.  每个插件，请调用[ **IPrintOemPrintTicketProvider::BindPrinter**](https://msdn.microsoft.com/library/windows/hardware/ff553151)。

3.  每个插件，请调用[ **IPrintOemPrintTicketProvider::QueryDeviceDefaultNamespace**](https://msdn.microsoft.com/library/windows/hardware/ff553180)。

 

 




