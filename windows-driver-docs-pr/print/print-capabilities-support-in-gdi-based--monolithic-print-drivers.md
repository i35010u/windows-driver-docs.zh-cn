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
ms.openlocfilehash: 8eb6d1e78739b08ecb87d06702ae89e801128926
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842349"
---
# <a name="print-capabilities-support-in-gdi-based-monolithic-print-drivers"></a>基于 GDI 的一体式打印驱动程序中的打印功能支持


若要提供完整的打印票证和打印功能支持，不能使用 GPD 打印机接口 DLL 的基于 GDI 的单一打印驱动程序和[XPSDrv 打印驱动程序](xpsdrv-printer-drivers.md)必须实现[IPrintTicketProvider 接口](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff554375(v=vs.85))。 不需要基于 GDI 的单一打印驱动程序来支持此接口，但这可能会限制在 PrintCapabilities 文档中公开并受 PrintTicket 文档支持的打印机功能。 但是，XPSDrv 打印驱动程序必须实现**IPrintTicketProvider**。

**注意**   适用于 Windows 7， **MxdcGetPDEVAdjustment**函数具有用于横向旋转的新参数。 有关详细信息，请参阅[**MxdcXDCGetPDEVAdjustment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mxdc/nf-mxdc-mxdcgetpdevadjustment)。

 

 

 




