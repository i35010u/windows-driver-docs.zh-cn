---
title: XPSDrv 的硬编码 UniDrv 和 PScript5 功能
description: XPSDrv 的硬编码 UniDrv 和 PScript5 功能
ms.assetid: d2922bc4-83d7-40da-adee-15c0810f2321
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2d9ed9ac627a98959a5d91e35afd9e3ded26c6f9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562881"
---
# <a name="hard-coded-unidrv-and-pscript5-features-for-xpsdrv"></a>XPSDrv 的硬编码 UniDrv 和 PScript5 功能


XPSDrv 模式中运行时，将禁用所有 Unidrv 或 PScript5 硬编码的功能。 Unidrv/PScript5 硬编码的功能是驱动程序的 GPD/PPD 文件没有指定的功能。

按以下方式禁用硬编码的功能：

-   功能不会显示在用户界面 (UI) Unidrv 或 PScript5 核心驱动程序中。

-   为 Microsoft Win32 DeviceCapabilities API、 Unidrv 或 PScript5 驱动程序的**DrvDeviceCapabilities**函数不会报告的硬编码的功能。

-   PrintCapabilities XML 不包含硬编码功能。

-   默认 Printticket 不包含硬编码功能的设置。

在本部分中进一步的其余主题描述在前面的区域中的基于 Unidrv/PScript5 XPSDrv 禁用硬编码功能的更改。

 

 




