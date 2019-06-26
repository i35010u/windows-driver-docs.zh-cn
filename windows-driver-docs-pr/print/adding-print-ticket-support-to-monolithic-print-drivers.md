---
title: 将打印票证支持添加到一体式打印驱动程序
description: 将打印票证支持添加到一体式打印驱动程序
ms.assetid: 82c65b9a-6e7b-4acd-93aa-33d696ddc421
keywords:
- 打印机接口 DLL WDK、 打印票证支持
- 整体化打印驱动程序 WDK
- 打印票证 WDK，整体化打印驱动程序
- IPrintTicketProvider
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aa4b3b4550eed074635933317951a291c23a46bc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382594"
---
# <a name="adding-print-ticket-support-to-monolithic-print-drivers"></a>将打印票证支持添加到一体式打印驱动程序


整体化打印驱动程序，以提供打印票证支持，并且支持[打印票证和打印功能技术](print-ticket-and-print-capabilities-technologies.md)，它必须实现[IPrintTicketProvider 接口](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff554375(v=vs.85))以及使用由打印驱动程序的 COM 样式调用方法为提供必要的 IClassFactory 接口支持。 最小值，该驱动程序必须支持在 OpenPrinter 期间调用 IPrintTicketProvider 接口的方法调用顺序如下所示：

1.  [GetSupportedVersions](getsupportedversions.md)

2.  [BindPrinter](bindprinter.md)

3.  [QueryDeviceNamespace](querydevicenamespace.md)

若要完成此接口的支持，打印驱动程序必须支持 IPrintTicketProvider 接口的方法的其余部分：

[GetPrintCapabilities](getprintcapabilities.md)

[ConvertDevModeToPrintTicket](convertdevmodetoprintticket2.md)

[ConvertPrintTicketToDevMode](convertprinttickettodevmode.md)

[ValidatePrintTicket](validateprintticket.md)

 

 




