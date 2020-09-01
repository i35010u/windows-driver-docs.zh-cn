---
title: 在 WMI 中注册和取消注册 NDIS 微型端口驱动程序
description: 在 WMI 中注册和取消注册 NDIS 微型端口驱动程序
ms.assetid: 7460cb3f-7dc1-4454-b683-e1849233fc1d
keywords:
- 微型端口适配器 WDK 网络，注册
- 适配器 WDK 网络，注册
- WMI WDK 网络，注册微型端口适配器
- 注册微型端口驱动程序
- 注册微型端口适配器
- 小型端口适配器 WDK 网络，WMI
- 适配器 WD
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 46ef277bb1350f15f60fbaa6de29f8b0c51dfe0a
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89211973"
---
# <a name="registration-and-deregistration-of-ndis-miniport-drivers-with-wmi"></a>在 WMI 中注册和取消注册 NDIS 微型端口驱动程序





NDIS 自动向 WMI 注册每个微型端口适配器。 小型小型驱动程序无需显式注册到 WMI，因为在微型端口驱动程序从 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize) 函数返回后，NDIS 会自动注册关联的微型端口适配器。

在使用 WMI 将某个微型端口适配器注册为数据提供程序后，WMI 客户端可以发送它查询并设置请求，并注册以接收状态指示。

在 NDIS 调用微型端口驱动程序的 [*MiniportHaltEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt) 函数之前，ndis 会自动通过 wmi 注销微型端口适配器，以便 wmi 不会再将 wmi 请求发送到微型端口驱动程序。

对于 NDIS 向 WMI 注册的每个微型端口适配器，NDIS 将注册对应于特定 Oid 或状态指示的 Guid。 NDIS 为微型端口适配器的支持的一组标准 Oid 和状态指示注册了 Guid。 有关这些标准 Guid 的详细信息，请参阅向 wmi [注册的标准微型端口驱动程序 oid](standard-miniport-driver-oids-registered-with-wmi.md) 和 [向 Wmi 注册的标准微型端口驱动程序状态](standard-miniport-driver-status-indications-registered-with-wmi.md)。

NDIS 还可以为自定义 Oid 和状态指示注册自定义 Guid。 如果微型端口驱动程序支持自定义 Oid，则它必须提供关联的自定义 Guid。 有关自定义 Oid 和状态指示的详细信息，请参阅 [自定义 oid 和状态指示](customized-oids-and-status-indications.md)。

对于面向连接的微型端口驱动程序，NDIS 还会)  (VCs 注册任何命名虚拟连接。 WMI 客户端只能与使用 [**NdisCoAssignInstanceName**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscoassigninstancename) 函数命名的独立调用管理器或面向连接的客户端的 VCs 配合使用。 有关对命名 VCs 的 NDIS WMI 支持的详细信息，请参阅 [对命名的 vcs 的支持](support-for-named-vcs.md)。

 

