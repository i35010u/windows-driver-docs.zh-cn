---
title: UPS 注册表项
description: UPS 注册表项
ms.assetid: d0d4ef8f-9df1-48a3-b0fc-cea4eb3cdf40
keywords:
- UPS 微型驱动程序 WDK，注册表项
- UPS 注册表项 WDK
- 注册表 WDK UPS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 494ef69cc0c7b632e5fa9f5fdaf9fa0ff897133b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533130"
---
# <a name="ups-registry-entries"></a>UPS 注册表项


## <span id="ddk_ups_registry_entries_kg"></span><span id="DDK_UPS_REGISTRY_ENTRIES_KG"></span>


UPS 注册表条目提供有关系统的 UPS 的特定于模型的信息。 供应商提供 UPS 微型驱动程序负责提供这些注册表项，将存储在 UPS 服务树的某些值。

以下注册表项是 UPS 服务树的根：

**HKEY\_LOCAL\_MACHINE**\\**SYSTEM**\\**CurrentControlSet**\\**Services**\\**UPS**

在以下四个项下组织 UPS 注册表项：

-   **UPS** -服务控制管理器项目，以及 Windows NT 4.0 UPS 服务所使用的项目

    这些项是仅供系统使用。 供应商不能修改这些条目。

-   **UPS**\\**Config** -UPS 服务的配置有关的信息。

    这些项是仅供系统使用。 供应商不能修改这些条目。

-   [UPS\\状态的注册表条目](ups-status-registry-entries.md)-状态信息。

    对于供应商和系统是使用这些条目。 如果供应商创建和修改这些条目，根据需要，**电源选项**显示它们。

-   [UPS\\ServiceProviders 注册表项](ups-serviceproviders-registry-entries.md)-为不同供应商和模型 UPS 设备条目。

    对于供应商和系统是使用这些条目。 供应商应创建这些项时[安装 UPS 微型驱动程序](installing-ups-minidrivers.md)。 管理员已选择使用 UPS 模型后，系统的 UPS 服务将 UPS 特定于模型的值复制到其他，控制系统的注册表位置。

 

 




