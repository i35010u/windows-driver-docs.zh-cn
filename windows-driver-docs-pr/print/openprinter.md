---
title: OpenPrinter
description: OpenPrinter
ms.assetid: 8bbb46a8-2bba-4d15-a2e2-4770b52d2505
keywords:
- OpenPrinter
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 03b116662632e42bc5e068060d5d83a6cdd8348f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385966"
---
# <a name="openprinter"></a>OpenPrinter


打开打印队列时 (通过使用`OpenPrinter`函数)，打印驱动程序加载和的以下方法[IPrintTicketProvider 接口](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff554375(v=vs.85))调用顺序如下：

1.  [**IPrintTicketProvider::GetSupportedVersions**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff554371(v=vs.85))

2.  [**IPrintTicketProvider::BindPrinter**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff554354(v=vs.85))

3.  [**IPrintTicketProvider::QueryDeviceNamespace**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff554378(v=vs.85))

方法**IPrintTicketProvider** Unidrv 或 PScript5 打印驱动程序调用中的接口**IPrintOemPrintTicketProvider**驱动程序由托管的每个插件方法。 下图和列表显示如何这些调用时将执行`OpenPrinter`调用。

![说明调用序列 openprinter 的关系图](images/ptpcopen-uml.gif)

1.  每个插件，请调用[ **IPrintOemPrintTicketProvider::GetSupportedVersions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemprintticketprovider-getsupportedversions)。

2.  每个插件，请调用[ **IPrintOemPrintTicketProvider::BindPrinter**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff553151(v=vs.85))。

3.  每个插件，请调用[ **IPrintOemPrintTicketProvider::QueryDeviceDefaultNamespace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemprintticketprovider-querydevicedefaultnamespace)。

 

 




