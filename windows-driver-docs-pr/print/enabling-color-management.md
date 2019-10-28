---
title: 启用颜色管理
description: 启用颜色管理
ms.assetid: 750d1e44-6d1c-4f18-94cb-20f1f846c0d1
keywords:
- 颜色管理 WDK 打印，启用
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c174a4a0d7dcdb50be304975a2e1202908330396
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838102"
---
# <a name="enabling-color-management"></a>启用颜色管理





应用程序或打印机驱动程序可以启用颜色管理。 应用程序可以通过以下两种方法之一启用颜色管理：

-   调用**SetICMMode** （如 Microsoft Windows SDK 文档中所述），并在上指定 ICM\_。

    此方法可实现系统控制的颜色管理。

-   在调用**CreateDC**创建打印作业时指定[**DEVMODEW**](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-_devicemodew)结构，并在 DEVMODE 结构的**DMICMMETHOD**中设置 DMICMMETHOD\_SYSTEM、DMICMMETHOD\_驱动程序或 DMICMMETHOD\_设备职员.

    此方法允许应用程序选择系统控制的、驱动程序控制的或设备控制的颜色管理（假定指定的控件类型受支持）。

打印机驱动程序可以通过在驱动程序的默认 DEVMODE 结构的**DMICMMETHOD**成员中设置 DMICMMETHOD\_SYSTEM、DMICMMETHOD\_DRIVER 或 DMICMMETHOD\_设备来启用颜色管理。 （如果为**CreateDC**提供 DEVMODE 结构，应用程序可以重写默认设置。 此外，该驱动程序负责在执行驱动程序的[**DrvDocumentPropertySheets**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvdocumentpropertysheets)函数的过程中存储用户选择的颜色管理。）

 

 




