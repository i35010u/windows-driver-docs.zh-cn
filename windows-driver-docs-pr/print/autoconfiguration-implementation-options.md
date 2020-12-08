---
title: 自动配置实现选项
description: 自动配置实现选项
keywords:
- 自动配置 WDK 打印机，实现选项
- 打印机自动配置 WDK 打印机，实现选项
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: de909cd9869a2e25f75ff46be65970400ba2efda
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836085"
---
# <a name="autoconfiguration-implementation-options"></a>自动配置实现选项


打印机供应商无需为自动配置提供支持。 Microsoft 不会修改现有的内置驱动程序，但鼓励 Ihv 为 Windows Vista 更新其驱动程序并包括对自动配置的支持。

对于选择支持自动配置的 Ihv，驱动程序和相关软件必须满足特定要求，无论此软件是否随 Windows 一起提供。

支持自动配置的要求取决于打印机驱动程序的实现方式，无论是打印机驱动程序的实现方式，也可以是打印机驱动程序的微型驱动程序，也可以是包含自定义端口监视器的方式。

<a href="" id="minidriver-implementation--custom-extensions-to-a-microsoft-printer-class-driver-or-a-microsoft-port-monitor-"></a>微型驱动程序实现 (Microsoft 打印机类驱动程序或 Microsoft 端口监视器的自定义扩展)   
请参阅 [自动配置的内置支持](in-box-support-for-autoconfiguration.md)

<a href="" id="monolithic-implementation--standalone-printer-driver-"></a>单独实现 (独立打印机驱动程序)   
请参阅 [IHV 驱动程序中的自动配置](autoconfiguration-in-an-ihv-driver.md)

<a href="" id="custom-port-monitor"></a>自定义端口监视器  
请参阅 [IHV 端口监视器中的自动配置](autoconfiguration-in-an-ihv-port-monitor.md)

**注意**   "Microsoft 打印机类驱动程序" 是指基于 Unidrv 或 Pscript5 的打印机驱动程序。 "Microsoft 端口监视器" 指的是标准 TCP/IP 端口监视器或用于设备的 Web 服务 (WSD) 端口监视器。

 

 

 




