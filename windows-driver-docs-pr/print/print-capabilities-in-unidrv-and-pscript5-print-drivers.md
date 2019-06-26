---
title: Unidrv 和 PScript5 打印驱动程序中的打印功能
description: Unidrv 和 PScript5 打印驱动程序中的打印功能
ms.assetid: 70f8b846-3e05-4345-baad-a3db6b8df620
keywords:
- 打印功能 WDK，Unidrv
- 打印功能 WDK，PScript5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c2dbbfd665cd526b364151d49d1c1cf0edb20e56
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373777"
---
# <a name="print-capabilities-in-unidrv-and-pscript5-print-drivers"></a>Unidrv 和 PScript5 打印驱动程序中的打印功能


Unidrv 和 PScript5 微型驱动程序提供支持打印功能功能所需的打印票证和打印功能接口。 这些打印驱动程序提供打印票证和打印功能的支持中所述的功能[通用打印机说明 (GPD) 文件](introduction-to-gpd-files.md)或 PostScript 打印机的说明 (PPD) 文件，根据需要，是否功能信息是中的公共或私有部分[ **DEVMODEW** ](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-_devicemodew)结构。

[XPSDrv 打印驱动程序](xpsdrv-printer-drivers.md)还可用于 Unidrv 打印机配置 DLL 提供所需的支持，这两个基于 GDI 的打印机配置接口和[IPrintTicketProvider 接口](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff554375(v=vs.85))。 如果使用 Unidrv 配置 DLL，可以加快开发的基本功能的打印机的 XPSDrv 打印机驱动程序或直通打印驱动程序。

 

 




