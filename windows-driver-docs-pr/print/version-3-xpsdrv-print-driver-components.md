---
title: 版本 3 XPSDrv 打印驱动程序组件
description: 版本 3 XPSDrv 打印驱动程序组件
ms.assetid: 7eced017-a6a6-4fa5-8965-ff6655f86b8c
keywords:
- XPSDrv 的打印机驱动程序 WDK，配置模块
- 配置模块 WDK XPSDrv，版本 3 XPS 驱动程序
- 版本 3 的 XPS 驱动程序 WDK XPSDrv
- 转换呈现模块 WDK XPSDrv
- 版本 3 XPS 驱动程序 WDK XPSDrv 有关版本 3 XPS 驱动程序
- XPSDrv 的打印机驱动程序 WDK，版本 3 XPS 驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dcfab6011e6a34f20ba27ddb4e105b7ef612f231
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533978"
---
# <a name="version-3-xpsdrv-print-driver-components"></a>版本 3 XPSDrv 打印驱动程序组件


XPSDrv 打印机驱动程序的版本 3 组件包含一个配置模块和 aconversion 呈现模块。

打印驱动程序基于相同的体系结构更早版本 3 XPSDrv 配置模块打印驱动程序。 （Windows Vista 还支持通用打印驱动程序 (Unidrv) 和 PostScript (PScript5) 打印驱动程序的通用打印机定义 (GPD) 文件和 PostScript 打印机定义 (PPD) 文件，分别基于。 Windows Vista 还支持 Unidrv 或 PScript5 打印驱动程序配置插件和整体化打印驱动程序配置模块。）

Microsoft Win32 应用程序打印到 XPSDrv 打印驱动程序通过使用现有的 GDI 打印支持 API。 Microsoft 提供转换呈现模块创建 XPS 假脱机文件从传入的设备驱动程序接口 (DDI) 调用 GDI 发出。

下列主题介绍了 XPSDrv 配置问题：

[XPDDrv 驱动程序选项](xpsdrv-driver-options.md)

[XPSDrv 驱动程序要求](xpsdrv-driver-requirements.md)

[XPSDrv 驱动程序建议](xpsdrv-driver-recommendations.md)

[XPSDrv 驱动程序实现](xpsdrv-driver-implementation.md)

[基于 Unidrv 或 PScript5 基于 XPSDrv 驱动程序更改](unidrv-based-or-pscript5-based-xpsdrv-driver-changes.md)

 

 




