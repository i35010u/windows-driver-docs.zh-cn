---
title: XPS 打印机驱动程序 (XPSDrv)
description: XPSDrv 是增强的、 基于 GDI 的版本 3 打印机驱动程序在 Windows Vista 之前使用。
ms.assetid: 7567c514-3034-4db0-9622-31d14eb3772e
keywords:
- 打印机驱动程序 WDK，XPSDrv 的打印机驱动程序
- XPSDrv 的打印机驱动程序 WDK
- XPSDrv 的打印机驱动程序 WDK，有关 XPSDrv 的打印机驱动程序
- 配置模块 WDK XPSDrv
- 呈现模块 WDK XPSDrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f1efd2c4dae9ebefc57be5d9ef17fc19047eb2c0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390228"
---
# <a name="xps-printer-driver-xpsdrv"></a>XPS 打印机驱动程序 (XPSDrv)


XPS 打印机驱动程序 (XPSDrv) 是增强的、 基于 GDI 的版本 3 打印机驱动程序在 Windows Vista 之前使用。 XPSDrv 的打印机驱动程序 （如基于 GDI 的） 包含三个主要组件。

这些是 XPSDrv 打印机驱动程序的三个主要组件：

-   [XPSDrv 呈现器模块](xpsdrv-render-module.md)

-   [XPSDrv 配置模块](xpsdrv-configuration-module.md)

-   [XPSDrv 安装](xpsdrv-installation.md)

配置模块的 XPSDrv 打印机驱动程序提供了相同的功能的配置模块[打印机接口 DLL](printer-interface-dll.md)基于 GDI 的驱动程序，但 XPSDrv 配置模块还支持[打印票证和打印功能技术](print-ticket-and-print-capabilities-technologies.md)。

XPSDrv 打印机驱动程序的呈现器模块一定，不是，使用基于 GDI 的打印机驱动程序的基于 GDI 的呈现功能。 相反，XPSDrv 打印机驱动程序的呈现器模块包含零个或多个筛选器和一个配置文件，描述了每个筛选器的操作。 XPSDrv 打印机驱动程序的呈现模块中的筛选器也必须支持要正确处理打印机的打印作业的打印票证技术。

有关安装 XPSDrv 驱动程序的详细信息，请参阅[XPSDrv 安装](xpsdrv-installation.md)。

 

 




