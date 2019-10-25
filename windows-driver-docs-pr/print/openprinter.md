---
title: OpenPrinter
description: OpenPrinter
ms.assetid: 8bbb46a8-2bba-4d15-a2e2-4770b52d2505
keywords:
- OpenPrinter
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0247bdd77782ed2832d510a716c039942218cf84
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843058"
---
# <a name="openprinter"></a>OpenPrinter


打开打印队列（通过使用 `OpenPrinter` 函数）时，将加载打印驱动程序，并按以下顺序调用[IPrintTicketProvider 接口](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff554375(v=vs.85))的以下方法：

1.  [**IPrintTicketProvider::GetSupportedVersions**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff554371(v=vs.85))

2.  [**IPrintTicketProvider::BindPrinter**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff554354(v=vs.85))

3.  [**IPrintTicketProvider::QueryDeviceNamespace**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff554378(v=vs.85))

Unidrv 或 PScript5 打印驱动程序中的**IPrintTicketProvider**接口的方法调用驱动程序所承载的每个插件的**IPrintOemPrintTicketProvider**方法。 下图和列表显示了在调用 `OpenPrinter` 时如何进行这些调用。

![说明 openprinter 调用序列的关系图](images/ptpcopen-uml.gif)

1.  对于每个插件，请调用[**IPrintOemPrintTicketProvider：： GetSupportedVersions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemprintticketprovider-getsupportedversions)。

2.  对于每个插件，请调用[**IPrintOemPrintTicketProvider：： BindPrinter**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff553151(v=vs.85))。

3.  对于每个插件，请调用[**IPrintOemPrintTicketProvider：： QueryDeviceDefaultNamespace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemprintticketprovider-querydevicedefaultnamespace)。

 

 




