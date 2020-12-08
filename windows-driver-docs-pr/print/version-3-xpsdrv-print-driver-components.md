---
title: 版本 3 XPSDrv 打印驱动程序组件
description: 版本 3 XPSDrv 打印驱动程序组件
keywords:
- XPSDrv 打印机驱动程序 WDK，配置模块
- 配置模块 WDK XPSDrv，版本 3 XPS 驱动程序
- 版本 3 XPS 驱动程序 WDK XPSDrv
- 转换呈现模块 WDK XPSDrv
- 版本 3 XPS 驱动程序 WDK XPSDrv，关于版本 3 XPS 驱动程序
- XPSDrv 打印机驱动程序 WDK，版本 3 XPS 驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2ce13520445e014459b38a14b1c1084cb951068a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785823"
---
# <a name="version-3-xpsdrv-print-driver-components"></a>版本 3 XPSDrv 打印驱动程序组件


XPSDrv 打印驱动程序的版本3组件包含配置模块和 aconversion 呈现模块。

XPSDrv 打印驱动程序的配置模块基于与早期版本3打印驱动程序相同的体系结构。  (Windows Vista 还支持通用打印驱动程序 (Unidrv) 和 PostScript (PScript5) 基于通用打印机定义的打印驱动程序 (GPD) 文件和 PostScript 打印机定义 (PPD) 文件。 Windows Vista 还支持 Unidrv 或 PScript5 打印驱动程序配置插件和单片打印驱动程序配置模块。 ) 

Microsoft Win32 应用程序使用现有的 GDI 打印支持 API 打印到 XPSDrv 打印驱动程序。 Microsoft 提供的转换呈现模块从传入设备驱动程序接口创建一个 XPS 假脱机文件，该文件 (GDI 发出的 DDI) 调用。

以下主题介绍了 XPSDrv 配置问题：

[XPDDrv 驱动程序选项](xpsdrv-driver-options.md)

[XPSDrv 驱动程序要求](xpsdrv-driver-requirements.md)

[XPSDrv 驱动程序建议](xpsdrv-driver-recommendations.md)

[XPSDrv 驱动程序实现](xpsdrv-driver-implementation.md)

[基于 Unidrv 或基于 PScript5 的 XPSDrv 驱动程序更改](unidrv-based-or-pscript5-based-xpsdrv-driver-changes.md)

 

 




