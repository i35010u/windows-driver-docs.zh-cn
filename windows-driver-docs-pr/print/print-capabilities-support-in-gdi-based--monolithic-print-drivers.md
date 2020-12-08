---
title: 基于 GDI 的一体式打印驱动程序中的打印功能支持
description: 基于 GDI 的一体式打印驱动程序中的打印功能支持
keywords:
- 打印功能 WDK，基于 GDI 的单一打印驱动程序
- 基于 GDI 的单一打印驱动程序 WDK
- 单一打印驱动程序 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 206bd39a445396e635479d7ac50c0dd3bd14a06e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807497"
---
# <a name="print-capabilities-support-in-gdi-based-monolithic-print-drivers"></a>基于 GDI 的一体式打印驱动程序中的打印功能支持


若要提供完整的打印票证和打印功能支持，不能使用 GPD 打印机接口 DLL 的基于 GDI 的单一打印驱动程序和 [XPSDrv 打印驱动程序](xpsdrv-printer-drivers.md) 必须实现 [IPrintTicketProvider 接口](/previous-versions/windows/hardware/drivers/ff554375(v=vs.85))。 不需要基于 GDI 的单一打印驱动程序来支持此接口，但这可能会限制在 PrintCapabilities 文档中公开并受 PrintTicket 文档支持的打印机功能。 但是，XPSDrv 打印驱动程序必须实现 **IPrintTicketProvider**。

**注意**   对于 Windows 7， **MxdcGetPDEVAdjustment** 函数具有用于横向旋转的新参数。 有关详细信息，请参阅 [**MxdcXDCGetPDEVAdjustment**](/windows-hardware/drivers/ddi/mxdc/nf-mxdc-mxdcgetpdevadjustment)。

 

 

