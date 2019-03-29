---
title: XPSDrv 驱动程序选项
description: XPSDrv 驱动程序选项
ms.assetid: 51db3cce-a95a-4084-9927-542c2d06312a
keywords:
- 版本 3 的 XPS 驱动程序 WDK XPSDrv，选项
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3262266b384cd4db9201604e90318157590d6c40
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576546"
---
# <a name="xpsdrv-driver-options"></a>XPSDrv 驱动程序选项


可以使用以下方法之一来实现 XPSDrv 打印机驱动程序的配置模块：

<a href="" id="text-file-only-------"></a>**仅文本文件**   
配置模块由 GPD 或 PPD 文件定义，并使用 Undriv 或 PScript5 配置模块实现的所有配置函数。 文本文件的唯一方法提供了最快的开发时间和开发成本最低，但它具有有限的自定义项的支持。 此方法最适合用于 XPSDrv 传递或基本 XPSDrv 打印驱动程序。

<a href="" id="plug-in-------"></a>**插件**   
配置模块定义由 GPD 或 PPD 文件和一个或多个 Unidrv 或 PScript5 打印驱动程序配置插件。插件方法可以灵活地自定义配置行为和用户体验，同时依赖于所有其他方面的 Unidrv 或 PScript5 配置模块的某些方面。 此方法的所需的开发时间取决于所需的打印驱动程序自定义的程度。 此方法适合于所有类型的打印驱动程序。

此类的一个插件，Mxdwdui.dll，Microsoft 提供的启用配置的 Microsoft XPS 文档转换器 (MXDC) 通过[IPrintOemUIMXDC COM 接口](iprintoemuimxdc-com-interface.md)。 MXDC 从基于 GDI 的应用程序以生成 XPS 包将转换输出。 此插件来快速将功能添加到 XPS 驱动程序的使用率是举例说明如何使用你自己的插件。

<a href="" id="monolithic"></a>**整体化**  
完全定义并实施配置模块。 整体式方法通常是开销最高的方法，因为必须执行所有打印驱动程序开发和测试，但此方法还提供了充分进行自定义的机会。

 

 




