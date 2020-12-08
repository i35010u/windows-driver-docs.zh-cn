---
title: UPS 注册表项
description: UPS 注册表项
keywords:
- UPS 微型驱动程序 WDK，注册表项
- UPS 注册表项 WDK
- 注册表 WDK UPS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 65ff6bd900f1f0309b010942c09e73f1d255a863
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798653"
---
# <a name="ups-registry-entries"></a>UPS 注册表项


## <span id="ddk_ups_registry_entries_kg"></span><span id="DDK_UPS_REGISTRY_ENTRIES_KG"></span>


UPS 注册表项提供有关系统的 UPS 的特定于模型的信息。 供应商提供的微型驱动程序负责为其中某些注册表条目（存储在 UPS 服务的树下）提供值。

以下注册表项是 UPS 服务树的根：

**HKEY \_本地 \_ 计算机** \\ **系统** \\ **CurrentControlSet** \\ **服务** \\ **UPS**

UPS 注册表项按以下四个键组织：

-   **Ups** --服务控制管理器条目，以及 Windows NT 4.0 UPS 服务使用的条目

    这些项仅供系统使用。 供应商不得修改这些条目。

-   **UPS** \\**Config** --与 UPS 服务配置有关的信息。

    这些项仅供系统使用。 供应商不得修改这些条目。

-   [UPS \\状态注册表项](ups-status-registry-entries.md) -状态信息。

    这些条目适用于供应商和系统使用。 如果供应商根据需要创建和修改这些条目， **电源选项** 会显示这些条目。

-   [UPS \\ServiceProviders 注册表项](ups-serviceproviders-registry-entries.md) -用于不同供应商和型号 UPS 设备的条目。

    这些条目适用于供应商和系统使用。 供应商应该在 [安装 UPS 微型驱动程序](installing-ups-minidrivers.md)时创建这些条目。 系统的 UPS 服务在管理员选择了要使用的 UPS 模型后，将特定于模型的值复制到其他由系统控制的注册表位置。

 

 




