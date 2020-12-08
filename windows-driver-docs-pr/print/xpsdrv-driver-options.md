---
title: XPSDrv 驱动程序选项
description: XPSDrv 驱动程序选项
keywords:
- 版本 3 XPS 驱动程序 WDK XPSDrv，选项
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 59aee922948c15185b0b6119ebe3e381ede27e06
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785715"
---
# <a name="xpsdrv-driver-options"></a>XPSDrv 驱动程序选项


您可以使用以下方法之一来实现 XPSDrv 打印驱动程序的配置模块：

<a href="" id="text-file-only-------"></a>**仅文本文件**   
配置模块由 GPD 或 PPD 文件定义，并使用 Undriv 或 PScript5 配置模块来实现所有配置功能。 纯文本文件方法提供最快的开发时间和最低的开发成本，但它对自定义的支持有限。 此方法最适合用于 XPSDrv passthrough 或 basic XPSDrv 打印驱动程序。

<a href="" id="plug-in-------"></a>**插件**   
配置模块由 GPD 或 PPD 文件以及一个或多个 Unidrv 或 PScript5 打印驱动程序配置插件定义。利用插件方法，你可以灵活地自定义配置行为和用户体验的某些方面，同时依赖于 Unidrv 或 PScript5 配置模块来执行所有其他方面的操作。 此方法所需的开发时间取决于您所需的打印驱动程序的自定义程度。 此方法适用于所有类型的打印驱动程序。

Microsoft 提供了一个此类插件 Mxdwdui.dll，通过 [IPRINTOEMUIMXDC COM 接口](iprintoemuimxdc-com-interface.md) (MXDC) 启用配置 Microsoft XPS 文档转换器。 MXDC 转换基于 GDI 的应用程序的输出以生成 XPS 包。 此插件利用插件快速向 XPS 驱动程序添加功能的示例是可以使用自己的插件完成的操作。

<a href="" id="monolithic"></a>**集成**  
你完全定义并实现配置模块。 整体方法通常是成本最高的方法，因为您必须执行所有打印驱动程序开发和测试，但此方法还为自定义提供了最大机会。

 

 




