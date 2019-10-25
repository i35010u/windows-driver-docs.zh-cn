---
title: 打印票证接口和打印驱动程序插件
description: 打印票证接口和打印驱动程序插件
ms.assetid: 5c5237a1-f4ff-42f9-8992-753743fd5e15
keywords:
- IPrintTicketProvider
- IPrintOemPrintTicketProvider
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1fd64f326e84703f805fcb6dc76063bc4457bb53
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842341"
---
# <a name="print-ticket-interfaces-and-print-driver-plug-ins"></a>打印票证接口和打印驱动程序插件


本部分介绍[IPrintTicketProvider 接口](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff554375(v=vs.85))和[IPrintOemPrintTicketProvider 接口](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintoemprintticketprovider)如何处理 Unidrv 和 PScript5 打印驱动程序及其插件以及调用的应用程序级函数的上下文它们.

本部分介绍以下 Microsoft Win32 函数的上下文：

[OpenPrinter](openprinter.md)

[ConvertDevModeToPrintTicket](convertdevmodetoprintticket.md)

[ConvertPrintTicketToDevMode](convertprinttickettodevmode.md)

[ValidatePrintTicket](validateprintticket.md)

 

 




