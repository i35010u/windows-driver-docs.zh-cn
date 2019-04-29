---
title: 基于 GDI 的一体式打印驱动程序中的打印功能支持
description: 基于 GDI 的一体式打印驱动程序中的打印功能支持
ms.assetid: 4b8116a8-7aee-44cb-9c9d-560662b61073
keywords:
- 打印功能 WDK，基于 GDI 的整体化打印驱动程序
- 基于 GDI 的整体化打印驱动程序 WDK
- 整体化打印驱动程序 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a0d339396d0e671b55017365c5f59f2161be105
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389484"
---
# <a name="print-capabilities-support-in-gdi-based-monolithic-print-drivers"></a>基于 GDI 的一体式打印驱动程序中的打印功能支持


若要提供完成打印票证和打印功能支持，基于 GDI 的、 整体化打印驱动程序和[XPSDrv 打印驱动程序](xpsdrv-printer-drivers.md)，不能使用 DLL 必须实现 GPD 打印机接口[IPrintTicketProvider接口](https://msdn.microsoft.com/library/windows/hardware/ff554375)。 基于 GDI 的、 整体化打印驱动程序不需要支持此接口，尽管这可以限制公开 PrintCapabilities 文档中并受 PrintTicket 文档的打印机的功能。 XPSDrv 打印机驱动程序; 但是，必须实现**IPrintTicketProvider**。

**请注意**  适用于 Windows 7， **MxdcGetPDEVAdjustment**函数具有横向旋转的新参数。 有关详细信息，请参阅[ **MxdcXDCGetPDEVAdjustment**](https://msdn.microsoft.com/library/windows/hardware/ff557558)。

 

 

 




