---
title: Windows 打印路径概述
description: Windows 打印路径概述
keywords:
- XPSDrv 打印机驱动程序 WDK，打印路径
- 打印路径 WDK XPSDrv
- GDI 打印路径 WDK XPSDrv
- XPS 打印路径 WDK XPSDrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d66e6e92516351bb969143da6879af77f6fb47b0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785801"
---
# <a name="windows-print-path-overview"></a>Windows 打印路径概述

Windows 提供了两个主要的打印路径和两个附加的转换路径。 这两个主要打印路径为：

-   GDI 打印路径 (类似于 Windows Server 2003 打印路径) 。 此路径也称为 Win32 路径，并使用 GDI 图形 API 在 Win32 应用程序中发出。

-   XPS 打印路径。 此路径源自 WPF) 应用程序或 XPS 打印 API Windows Presentation Foundation (。

这两个转换选项为：

-   MXDC) 的 GDI 到 XPS 转换 (。

-    (XGC) 的 XPS 到 GDI 转换。

### <a name="general-data-flow"></a>一般数据流

下图显示了 XPSDrv 子系统的不同打印路径和转换选项。

![说明 xpsdrv 子系统的不同打印路径和转换选项的关系图](images/printpathoverview.png)

有关配置筛选器管道服务的详细信息，请参阅 [筛选器管道配置文件](filter-pipeline-configuration-file.md)。

有关为 Windows Vista 和更高版本的 Windows 配置版本3打印驱动程序的详细信息，请参阅 [版本 3 XPSDrv 打印驱动程序组件](version-3-xpsdrv-print-driver-components.md)。
