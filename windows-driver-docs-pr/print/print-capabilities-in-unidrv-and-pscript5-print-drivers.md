---
title: Unidrv 和 PScript5 打印驱动程序中的打印功能
description: Unidrv 和 PScript5 打印驱动程序中的打印功能
keywords:
- 打印功能 WDK，Unidrv
- 打印功能 WDK，PScript5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 16bce207bf84cbde69b82ba945a1aef34555f4cd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807499"
---
# <a name="print-capabilities-in-unidrv-and-pscript5-print-drivers"></a>Unidrv 和 PScript5 打印驱动程序中的打印功能


Unidrv 和 PScript5 微型驱动程序提供支持打印功能功能所需的打印票证和打印功能接口。 这些打印驱动程序针对 [一般打印机说明 (GPD) 文件](introduction-to-gpd-files.md) 或 PostScript 打印机说明 (PPD) 文件中所述的功能提供了打印票证和打印功能，这些功能是否适用于 [**DEVMODEW**](/windows/win32/api/wingdi/ns-wingdi-devmodew) 结构的公共或私有部分。

[XPSDrv 打印驱动程序](xpsdrv-printer-drivers.md) 还可以使用 Unidrv 打印机配置 DLL 为基于 GDI 的打印机配置接口和 [IPrintTicketProvider 接口](/previous-versions/windows/hardware/drivers/ff554375(v=vs.85))提供所需的支持。 如果使用 Unidrv 配置 DLL，则可以加速为基本功能打印机或直通打印驱动程序开发 XPSDrv 打印机驱动程序。

 

