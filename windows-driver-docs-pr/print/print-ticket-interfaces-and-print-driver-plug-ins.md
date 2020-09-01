---
title: 打印票证接口和打印驱动程序插件
description: 打印票证接口和打印驱动程序插件
ms.assetid: 5c5237a1-f4ff-42f9-8992-753743fd5e15
keywords:
- IPrintTicketProvider
- IPrintOemPrintTicketProvider
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f107e984cf1e660011f6b6adced30458edac64ac
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89207103"
---
# <a name="print-ticket-interfaces-and-print-driver-plug-ins"></a>打印票证接口和打印驱动程序插件


本部分介绍 [IPrintTicketProvider 接口](/previous-versions/windows/hardware/drivers/ff554375(v=vs.85)) 和 [IPrintOemPrintTicketProvider 接口](/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintoemprintticketprovider) 如何处理 Unidrv 和 PScript5 打印驱动程序及其插件以及调用它们的应用程序级函数的上下文。

本部分介绍以下 Microsoft Win32 函数的上下文：

[OpenPrinter](openprinter.md)

[ConvertDevModeToPrintTicket](convertdevmodetoprintticket.md)

[ConvertPrintTicketToDevMode](convertprinttickettodevmode.md)

[ValidatePrintTicket](validateprintticket.md)

 

