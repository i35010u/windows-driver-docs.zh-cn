---
title: OpenPrinter
description: OpenPrinter
ms.assetid: 8bbb46a8-2bba-4d15-a2e2-4770b52d2505
keywords:
- OpenPrinter
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b8173e7001e4bd4d5bb77c0f5e7d152043056907
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89207735"
---
# <a name="openprinter"></a>OpenPrinter


使用函数)  (打开打印队列时，将 `OpenPrinter` 加载打印驱动程序，并按以下顺序调用 [IPrintTicketProvider 接口](/previous-versions/windows/hardware/drivers/ff554375(v=vs.85)) 的以下方法：

1.  [**IPrintTicketProvider::GetSupportedVersions**](/previous-versions/windows/hardware/drivers/ff554371(v=vs.85))

2.  [**IPrintTicketProvider::BindPrinter**](/previous-versions/windows/hardware/drivers/ff554354(v=vs.85))

3.  [**IPrintTicketProvider::QueryDeviceNamespace**](/previous-versions/windows/hardware/drivers/ff554378(v=vs.85))

Unidrv 或 PScript5 打印驱动程序中的 **IPrintTicketProvider** 接口的方法调用驱动程序所承载的每个插件的 **IPrintOemPrintTicketProvider** 方法。 下图和列表显示了调用时如何进行这些调用 `OpenPrinter` 。

![说明 openprinter 调用序列的关系图](images/ptpcopen-uml.gif)

1.  对于每个插件，请调用 [**IPrintOemPrintTicketProvider：： GetSupportedVersions**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemprintticketprovider-getsupportedversions)。

2.  对于每个插件，请调用 [**IPrintOemPrintTicketProvider：： BindPrinter**](/previous-versions/windows/hardware/drivers/ff553151(v=vs.85))。

3.  对于每个插件，请调用 [**IPrintOemPrintTicketProvider：： QueryDeviceDefaultNamespace**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemprintticketprovider-querydevicedefaultnamespace)。

 

