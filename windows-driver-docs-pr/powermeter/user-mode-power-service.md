---
title: 用户模式下 Power 服务
description: 用户模式下 Power 服务
ms.assetid: 57f3affd-18cc-440c-ba18-9ba89fd3c84f
keywords:
- 电源计量和预算 WDK，用户模式下 Power 服务
- 用户模式服务 WDK Power 电表
- UMPS WDK 电源表
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 30d03f1e10a009d8c169b71457287a6fce2deb83
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540721"
---
# <a name="user-mode-power-service"></a>用户模式下 Power 服务


从 Windows 7 和 Windows Server 2008 R2 开始，用户模式下 Power 服务 (UMPS) 提供用于对用户模式服务和应用程序的电源管理的所有方面的接口。 此接口包含对能源计量和预算 (PMB) 基础结构与电源相关信息的支持。 应用程序，如 Windows 性能监视器 (PerfMon)，使用此信息有关电源管理和报告。

UMPS 通过使用一组 PMB WMI 类提供对 PMB 信息的访问。 这些 WMI 类符合版本 1.1.0 的分布式管理任务组 (DMTF) 电源提供配置文件。 有关详细信息，请参阅[DMTF 电源提供配置文件](https://go.microsoft.com/fwlink/p/?linkid=145048)。

PMB WMI 类提供以下支持：

-   当前的能源计量和预算 power 测定仪设备信息的查询。

-   当超过测定仪的功率阈值或预算时注册的回调通知。

当 UPMS PMB WMI 请求提供服务时，它将调用通过 I/O 请求数据包 (Irp) 支持的 PMI 到电源计量接口 (PMI)。 有关 PMI 详细信息，请参阅[电源计量接口](power-meter-interface.md)。

有关 PMB WMI 类的详细信息，请参阅 Windows SDK 文档。

 

 




