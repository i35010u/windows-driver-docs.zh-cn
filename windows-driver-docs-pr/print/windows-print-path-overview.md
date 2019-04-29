---
title: Windows 打印路径概述
description: Windows 打印路径概述
ms.assetid: c06e122b-a4d8-4b3a-9db0-0bc8f2728177
keywords:
- XPSDrv 的打印机驱动程序 WDK，打印路径
- 打印路径 WDK XPSDrv
- GDI 打印路径 WDK XPSDrv
- XPS 打印路径 WDK XPSDrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 848068adda4ac0f0e310ef4c24fca5bc65707aef
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370377"
---
# <a name="windows-print-path-overview"></a>Windows 打印路径概述

Windows 提供了两个主要的打印路径和两个附加的转换路径。 两个主要的打印路径是：

-   GDI 打印路径 （类似于 Windows Server 2003 打印路径）。 此路径也称为 Win32 路径，源自在 Win32 应用程序中使用的 GDI 图形 API。

-   XPS 打印路径。 此路径之后，在 Windows Presentation Foundation (WPF) 应用程序中或从 XPS 打印 API。

两个转换选项包括：

-   GDI 到 XPS 的转换 (MXDC)。

-   XPS GDI 转换 (XGC)。

### <a name="general-data-flow"></a>一般情况下数据 Flow

下图显示了不同的打印 XPSDrv 子系统的路径和转换选项。

![说明 xpsdrv 子系统的不同的打印路径和转换选项的关系图](images/printpathoverview.png)

有关配置筛选器管道服务的详细信息，请参阅[筛选器管道配置文件](filter-pipeline-configuration-file.md)。

有关配置的版本 3 打印驱动程序适用于 Windows Vista 和更高版本的 Windows 的详细信息，请参阅[版本 3 XPSDrv 打印驱动程序组件](version-3-xpsdrv-print-driver-components.md)。
