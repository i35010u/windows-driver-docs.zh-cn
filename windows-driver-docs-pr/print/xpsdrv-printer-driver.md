---
title: XPS 打印机驱动程序 (XPSDrv)
description: XPSDrv 是在 Windows Vista 之前使用的基于 GDI 的增强版本3打印机驱动程序。
keywords:
- 打印机驱动程序 WDK，XPSDrv 打印机驱动程序
- XPSDrv 打印机驱动程序 WDK
- XPSDrv 打印机驱动程序 WDK，关于 XPSDrv 打印机驱动程序
- 配置模块 WDK XPSDrv
- 渲染模块 WDK XPSDrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 98bccbdfc851bf2143e2a3b0763929ae9ae5f2dc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785701"
---
# <a name="xps-printer-driver-xpsdrv"></a>XPS 打印机驱动程序 (XPSDrv)


XPS 打印机驱动程序 (XPSDrv) 是在 Windows Vista 之前使用的、基于 GDI 的增强版本3打印机驱动程序。 XPSDrv 打印机驱动程序 (例如基于 GDI 的驱动程序) 由三个主要组件组成。

这是 XPSDrv 打印机驱动程序的三个主要组件：

-   [XPSDrv 渲染器模块](xpsdrv-render-module.md)

-   [XPSDrv 配置模块](xpsdrv-configuration-module.md)

-   [XPSDrv 安装](xpsdrv-installation.md)

XPSDrv 打印机驱动程序的配置模块提供与基于 GDI 的驱动程序的 [打印机接口 DLL](printer-interface-dll.md) 的配置模块相同的功能，但 XPSDrv 配置模块还支持 [打印票证和打印功能技术](print-ticket-and-print-capabilities-technologies.md)。

XPSDrv 打印机驱动程序的渲染模块并不一定要使用基于 gdi 的打印机驱动程序的基于 GDI 的着色功能。 相反，XPSDrv 打印机驱动程序的呈现模块由零个或多个筛选器以及描述每个筛选器的操作的配置文件组成。 XPSDrv 打印机驱动程序的呈现模块中的筛选器还必须支持打印票证技术，才能正确地处理打印机的打印作业。

有关安装 XPSDrv 驱动程序的详细信息，请参阅 [XPSDrv 安装](xpsdrv-installation.md)。

 

 




