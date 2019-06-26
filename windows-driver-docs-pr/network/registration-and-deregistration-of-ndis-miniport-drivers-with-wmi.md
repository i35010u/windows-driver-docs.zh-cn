---
title: 在 WMI 中注册和取消注册 NDIS 微型端口驱动程序
description: 在 WMI 中注册和取消注册 NDIS 微型端口驱动程序
ms.assetid: 7460cb3f-7dc1-4454-b683-e1849233fc1d
keywords:
- 微型端口适配器 WDK 连接网络、 注册
- 适配器 WDK 连接网络、 注册
- WMI WDK 连接网络、 注册微型端口适配器
- 注册微型端口驱动程序
- 注册微型端口适配器
- 微型端口适配器 WDK 网络 WMI
- 适配器 WD
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c7757458634583a4d282fb8eb9ad43d177b52120
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374742"
---
# <a name="registration-and-deregistration-of-ndis-miniport-drivers-with-wmi"></a>在 WMI 中注册和取消注册 NDIS 微型端口驱动程序





NDIS 自动向 WMI 注册每个微型端口适配器。 微型端口驱动程序不必显式注册到 WMI，因为 NDIS 自动注册为关联的微型端口适配器从微型端口驱动程序返回后[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)函数。

NDIS 将微型端口适配器注册为 wmi 数据提供程序后，WMI 客户端可以将其发送查询并将请求设置并注册以获得状态指示。

NDIS 调用微型端口驱动程序的前[ *MiniportHaltEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt)函数，NDIS 自动注销与 WMI 的微型端口适配器，因此 WMI 将无法再将 WMI 请求发送到微型端口驱动程序。

对于每个向 WMI 注册 NDIS 的微型端口适配器，NDIS 注册与特定 Oid 或状态指示相对应的 Guid。 NDIS 注册微型端口适配器的支持的标准 Oid 和状态指示集的 Guid。 有关这些标准 Guid 的详细信息，请参阅[标准微型端口驱动程序 Oid 注册与 WMI 配合](standard-miniport-driver-oids-registered-with-wmi.md)并[标准微型端口驱动程序状态已注册与 WMI](standard-miniport-driver-status-indications-registered-with-wmi.md)。

NDIS 还可以自定义 Oid 和状态指示注册自定义 Guid。 如果微型端口驱动程序支持自定义 Oid，它必须提供相关联的自定义 Guid。 有关自定义的 Oid 和状态指示的详细信息，请参阅[自定义 Oid 和状态指示](customized-oids-and-status-indications.md)。

有关面向连接的微型端口驱动程序，NDIS 还会注册任何命名的虚拟连接 (VCs)。 WMI 客户端仅可以使用独立的呼叫管理器或面向连接的客户端具有名为 VCs [ **NdisCoAssignInstanceName** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscoassigninstancename)函数。 有关命名 VCs 的 NDIS WMI 支持的详细信息，请参阅[支持名为 VCs](support-for-named-vcs.md)。

 

 





