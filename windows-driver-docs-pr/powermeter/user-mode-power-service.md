---
title: 用户模式功率服务
description: 用户模式功率服务
keywords:
- 电源计量和预算 WDK，User-Mode 电源服务
- User-Mode 电源服务 WDK 电源指示器
- UMPS WDK 电源计量器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cf672c6b09e1ed0436e6c5df4e0b42dc487baade
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812467"
---
# <a name="user-mode-power-service"></a>用户模式功率服务


从 Windows 7 和 Windows Server 2008 R2 开始，User-Mode 电源服务 (UMPS) 为用户模式服务和应用程序的电源管理的所有方面提供了一个接口。 此接口包含对电源相关信息的电源计量和预算 (PMB) 基础结构的支持。 此信息由应用程序使用，例如 Windows 性能监视器 (PerfMon) ，用于电源管理和报告。

通过使用一组 PMB WMI 类，UMPS 提供对 PMB 信息的访问。 这些 WMI 类符合分布式管理任务组 (DMTF) 电源配置文件的版本1.1.0。 有关详细信息，请参阅 [DMTF 电源配置文件](https://go.microsoft.com/fwlink/p/?linkid=145048)。

PMB WMI 类提供对以下各项的支持：

-   查询电源计量设备的当前电源计量和预算信息。

-   当指示器的电量阈值或预算超出时，注册回调通知。

当 UPMS services PMB WMI 请求时，它会调入 (PMI) ，通过使用 PMI 支持的 (Irp) 中的 i/o 请求数据包来。 有关 PMI 的详细信息，请参阅 [电源指示器界面](power-meter-interface.md)。

有关 PMB WMI 类的详细信息，请参阅 Windows SDK 文档。

 

 




