---
title: 打印票证接口和打印驱动程序插件
description: 打印票证接口和打印驱动程序插件
keywords:
- IPrintTicketProvider
- IPrintOemPrintTicketProvider
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c2c2ec019291c97e10cc9eece0e9a9e8b3b451b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807415"
---
# <a name="print-ticket-interfaces-and-print-driver-plug-ins"></a>打印票证接口和打印驱动程序插件


本部分介绍 [IPrintTicketProvider 接口](/previous-versions/windows/hardware/drivers/ff554375(v=vs.85)) 和 [IPrintOemPrintTicketProvider 接口](/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintoemprintticketprovider) 如何处理 Unidrv 和 PScript5 打印驱动程序及其插件以及调用它们的应用程序级函数的上下文。

本部分介绍以下 Microsoft Win32 函数的上下文：

[OpenPrinter](openprinter.md)

[ConvertDevModeToPrintTicket](convertdevmodetoprintticket.md)

[ConvertPrintTicketToDevMode](convertprinttickettodevmode.md)

[ValidatePrintTicket](validateprintticket.md)

 

