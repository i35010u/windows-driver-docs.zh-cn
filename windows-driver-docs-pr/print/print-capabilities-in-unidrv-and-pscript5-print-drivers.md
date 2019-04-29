---
title: Unidrv 和 PScript5 打印驱动程序中的打印功能
description: Unidrv 和 PScript5 打印驱动程序中的打印功能
ms.assetid: 70f8b846-3e05-4345-baad-a3db6b8df620
keywords:
- 打印功能 WDK，Unidrv
- 打印功能 WDK，PScript5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 327886f212ca8e6ec85a6da22098bd8c8c24024a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389485"
---
# <a name="print-capabilities-in-unidrv-and-pscript5-print-drivers"></a>Unidrv 和 PScript5 打印驱动程序中的打印功能


Unidrv 和 PScript5 微型驱动程序提供支持打印功能功能所需的打印票证和打印功能接口。 这些打印驱动程序提供打印票证和打印功能的支持中所述的功能[通用打印机说明 (GPD) 文件](introduction-to-gpd-files.md)或 PostScript 打印机的说明 (PPD) 文件，根据需要，是否功能信息是中的公共或私有部分[ **DEVMODEW** ](https://msdn.microsoft.com/library/windows/hardware/ff552837)结构。

[XPSDrv 打印驱动程序](xpsdrv-printer-drivers.md)还可用于 Unidrv 打印机配置 DLL 提供所需的支持，这两个基于 GDI 的打印机配置接口和[IPrintTicketProvider 接口](https://msdn.microsoft.com/library/windows/hardware/ff554375)。 如果使用 Unidrv 配置 DLL，可以加快开发的基本功能的打印机的 XPSDrv 打印机驱动程序或直通打印驱动程序。

 

 




