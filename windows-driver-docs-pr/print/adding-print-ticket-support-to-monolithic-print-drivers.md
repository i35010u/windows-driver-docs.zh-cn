---
title: 将打印票证支持添加到一体式打印驱动程序
description: 将打印票证支持添加到一体式打印驱动程序
ms.assetid: 82c65b9a-6e7b-4acd-93aa-33d696ddc421
keywords:
- 打印机接口 DLL WDK，打印票证支持
- 单一打印驱动程序 WDK
- 打印入场券 WDK，单片打印驱动程序
- IPrintTicketProvider
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1797e617948b8c8d421f8fd56f65374e56ced1b7
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89218274"
---
# <a name="adding-print-ticket-support-to-monolithic-print-drivers"></a>将打印票证支持添加到一体式打印驱动程序


为了使单个打印驱动程序提供打印票证支持并支持 [打印票证和打印功能技术](print-ticket-and-print-capabilities-technologies.md)，它必须实现 [IPrintTicketProvider 接口](/previous-versions/windows/hardware/drivers/ff554375(v=vs.85)) ，并为打印驱动程序使用的 COM 样式调用方法提供必要的 IClassFactory 接口支持。 驱动程序至少必须支持 IPrintTicketProvider 接口的方法，这些方法在 OpenPrinter 调用期间按下面所示的顺序调用：

1.  [GetSupportedVersions](getsupportedversions.md)

2.  [BindPrinter](bindprinter.md)

3.  [QueryDeviceNamespace](querydevicenamespace.md)

若要完成对此接口的支持，打印驱动程序必须支持 IPrintTicketProvider 接口的其余方法：

[GetPrintCapabilities](getprintcapabilities.md)

[ConvertDevModeToPrintTicket](convertdevmodetoprintticket2.md)

[ConvertPrintTicketToDevMode](convertprinttickettodevmode.md)

[ValidatePrintTicket](validateprintticket.md)

 

