---
title: 基于 GDI 的一体式打印驱动程序中的打印功能支持
description: 基于 GDI 的一体式打印驱动程序中的打印功能支持
ms.assetid: 4b8116a8-7aee-44cb-9c9d-560662b61073
keywords:
- 打印功能 WDK，基于 GDI 的单一打印驱动程序
- 基于 GDI 的单一打印驱动程序 WDK
- 单一打印驱动程序 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 85cb6dceed1f3c9eb3f883699db130f192e89216
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89214212"
---
# <a name="print-capabilities-support-in-gdi-based-monolithic-print-drivers"></a>基于 GDI 的一体式打印驱动程序中的打印功能支持


若要提供完整的打印票证和打印功能支持，不能使用 GPD 打印机接口 DLL 的基于 GDI 的单一打印驱动程序和 [XPSDrv 打印驱动程序](xpsdrv-printer-drivers.md) 必须实现 [IPrintTicketProvider 接口](/previous-versions/windows/hardware/drivers/ff554375(v=vs.85))。 不需要基于 GDI 的单一打印驱动程序来支持此接口，但这可能会限制在 PrintCapabilities 文档中公开并受 PrintTicket 文档支持的打印机功能。 但是，XPSDrv 打印驱动程序必须实现 **IPrintTicketProvider**。

**注意**   对于 Windows 7， **MxdcGetPDEVAdjustment**函数具有用于横向旋转的新参数。 有关详细信息，请参阅 [**MxdcXDCGetPDEVAdjustment**](/windows-hardware/drivers/ddi/mxdc/nf-mxdc-mxdcgetpdevadjustment)。

 

 

