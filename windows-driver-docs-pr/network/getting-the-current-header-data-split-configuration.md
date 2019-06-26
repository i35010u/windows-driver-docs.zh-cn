---
title: 获取当前的标头数据拆分配置
description: 获取当前的标头数据拆分配置
ms.assetid: 62c5e362-4e19-465d-85a8-a8277cb46f5d
keywords:
- 标头数据拆分 WDK、 配置
- 当前标头数据拆分配置 WDK 网络
- 状态信息 WDK 标头数据拆分
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 447fda131cd2c3049420a689da23be01de1002cc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382751"
---
# <a name="getting-the-current-header-data-split-configuration"></a>获取当前的标头数据拆分配置





若要获取当前标头数据拆分微型端口适配器，过量驱动程序的设置或用户模式应用程序可以查询[OID\_代\_HD\_拆分\_当前\_配置](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-hd-split-current-config) OID。 但是，过量驱动程序应使用 NDIS 可用于向其在初始化期间，状态指示的信息。

系统管理员可以使用与 OID 关联的 GUID\_GEN\_HD\_拆分\_当前\_通过 WMI 界面配置 OID。 有关详细信息标头数据拆分 WMI Guid，请参阅[标头数据拆分为 WMI 支持](wmi-support-for-header-data-split.md)。

NDIS 句柄[OID\_代\_HD\_拆分\_当前\_配置](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-hd-split-current-config)代表微型端口驱动程序。 NDIS 维护当前的标头数据拆分基于微型端口驱动程序初始化属性的配置信息并[ **NDIS\_状态\_HD\_拆分\_当前\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-hd-split-current-config)状态指示。

**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构包含[ **NDIS\_HD\_拆分\_当前\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_hd_split_current_config)结构。 NDIS 还提供了 NDIS\_HD\_拆分\_当前\_到在初始化过程并通过状态指示过量驱动程序的配置结构。

当微型端口驱动程序收到[OID\_代\_HD\_拆分\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-hd-split-parameters)集请求，该驱动程序必须使用的内容[ **NDIS\_HD\_拆分\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_hd_split_parameters)结构，以更新当前的微型端口适配器配置。 更新后，微型端口驱动程序必须报告更改，并[ **NDIS\_状态\_HD\_拆分\_当前\_配置**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-hd-split-current-config)状态指示。 状态指示可确保所有基础驱动程序更新使用新的信息。

当调用 NDIS [ *ProtocolBindAdapterEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_bind_adapter_ex)函数的 NDIS 6.1 或更高版本协议驱动程序，NDIS 提供[ **NDIS\_绑定\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_bind_parameters)用一个指针指向的结构[ **NDIS\_HD\_拆分\_当前\_配置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_hd_split_current_config)结构。

当调用 NDIS [ *FilterAttach* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_attach) NDIS 6.1 或更高版本筛选器驱动程序，NDIS 函数提供[ **NDIS\_筛选器\_附加\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_filter_attach_parameters)结构的指针到 NDIS\_HD\_拆分\_当前\_配置结构。

 

 





