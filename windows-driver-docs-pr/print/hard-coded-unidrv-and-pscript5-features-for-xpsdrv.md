---
title: XPSDrv 的硬编码 UniDrv 和 PScript5 功能
description: XPSDrv 的硬编码 UniDrv 和 PScript5 功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fa7782f821de2951aed1429e10cf8b2ca38f01b6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835833"
---
# <a name="hard-coded-unidrv-and-pscript5-features-for-xpsdrv"></a>XPSDrv 的硬编码 UniDrv 和 PScript5 功能


在 XPSDrv 模式下运行时，所有 Unidrv 或 PScript5 硬编码功能都处于禁用状态。 Unidrv/PScript5 硬编码功能是驱动程序的 GPD/PPD 文件未指定的功能。

硬编码功能的禁用方式如下：

-   此功能不会显示在 Unidrv 或 PScript5 核心驱动程序 (UI) 的任何用户界面中。

-   对于 Microsoft Win32 DeviceCapabilities API，Unidrv 或 PScript5 驱动程序的 **DrvDeviceCapabilities** 函数不报告硬编码功能。

-   PrintCapabilities XML 不包含硬编码功能。

-   默认 Printticket 不包含硬编码功能的设置。

本部分中的其余主题进一步介绍了前面几个区域中基于 Unidrv/PScript5 的 XPSDrv 禁用硬编码功能所做的更改。

 

 




