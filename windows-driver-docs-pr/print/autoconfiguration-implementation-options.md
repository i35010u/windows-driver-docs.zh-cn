---
title: 自动配置实现选项
description: 自动配置实现选项
ms.assetid: 78a4e11c-ee6e-4306-b787-2ff7889ff877
keywords:
- 自动配置 WDK 打印机，实现选项
- 打印机自动配置 WDK 打印机，实现选项
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 56e7d4fcb56bc79d60d7412cadbe2079b06352aa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523996"
---
# <a name="autoconfiguration-implementation-options"></a>自动配置实现选项


打印机供应商不需要为自动配置提供支持。 Microsoft 将不会修改现有的现成驱动程序，但 Ihv 建议适用于 Windows Vista 更新其驱动程序，包括对自动配置的支持。

是否支持自动配置，驱动程序和相关的软件必须满足特定要求进行选择的 ihv 此软件提供现成的 Windows。

支持自动配置的要求取决于打印机驱动程序的实现方式-作为打印机微型驱动程序或整体式打印机驱动程序，以及是否包括自定义端口监视器。

<a href="" id="minidriver-implementation--custom-extensions-to-a-microsoft-printer-class-driver-or-a-microsoft-port-monitor-"></a>微型驱动程序实现 （自定义扩展到 Microsoft 打印机类驱动程序或 Microsoft 端口监视器）  
请参阅[框自动配置的支持](in-box-support-for-autoconfiguration.md)

<a href="" id="monolithic-implementation--standalone-printer-driver-"></a>整体化实现 （独立的打印机驱动程序）  
请参阅[IHV 驱动程序中的自动配置](autoconfiguration-in-an-ihv-driver.md)

<a href="" id="custom-port-monitor"></a>自定义端口监视器  
请参阅[IHV 端口监视器中的自动配置](autoconfiguration-in-an-ihv-port-monitor.md)

**请注意**   "Microsoft 打印机类驱动程序"是指基于 Unidrv 或基于 Pscript5 的打印机驱动程序。 "Microsoft 端口监视器"是指标准 TCP/IP 端口监视器或 Web Services for Devices (WSD) 端口监视器。

 

 

 




