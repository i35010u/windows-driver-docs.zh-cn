---
title: 添加对整体化打印驱动程序的打印票证支持
description: 添加对整体化打印驱动程序的打印票证支持
ms.assetid: 82c65b9a-6e7b-4acd-93aa-33d696ddc421
keywords:
- 打印机接口 DLL WDK、 打印票证支持
- 整体化打印驱动程序 WDK
- 打印票证 WDK，整体化打印驱动程序
- IPrintTicketProvider
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f267349111f0c5059197d720479957a1afc7ab5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542218"
---
# <a name="adding-print-ticket-support-to-monolithic-print-drivers"></a>添加对整体化打印驱动程序的打印票证支持


整体化打印驱动程序，以提供打印票证支持，并且支持[打印票证和打印功能技术](print-ticket-and-print-capabilities-technologies.md)，它必须实现[IPrintTicketProvider 接口](https://msdn.microsoft.com/library/windows/hardware/ff554375)以及使用由打印驱动程序的 COM 样式调用方法为提供必要的 IClassFactory 接口支持。 最小值，该驱动程序必须支持在 OpenPrinter 期间调用 IPrintTicketProvider 接口的方法调用顺序如下所示：

1.  [GetSupportedVersions](getsupportedversions.md)

2.  [BindPrinter](bindprinter.md)

3.  [QueryDeviceNamespace](querydevicenamespace.md)

若要完成此接口的支持，打印驱动程序必须支持 IPrintTicketProvider 接口的方法的其余部分：

[GetPrintCapabilities](getprintcapabilities.md)

[ConvertDevModeToPrintTicket](convertdevmodetoprintticket2.md)

[ConvertPrintTicketToDevMode](convertprinttickettodevmode.md)

[ValidatePrintTicket](validateprintticket.md)

 

 




