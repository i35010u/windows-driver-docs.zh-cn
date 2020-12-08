---
title: 获取当前的标头数据拆分配置
description: 获取当前的标头数据拆分配置
keywords:
- 标头-数据拆分 WDK，配置
- 当前标头-数据拆分配置 WDK 网络
- 状态信息 WDK 标头-数据拆分
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7348120670309aedf57d00e8229faaf72c976be7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817149"
---
# <a name="getting-the-current-header-data-split-configuration"></a>获取当前的标头数据拆分配置





为了获取微型端口适配器的当前标头-数据拆分设置，过量驱动程序或用户模式应用程序可以查询 [OID \_ 生成 \_ HD \_ split \_ 当前 \_ 配置](./oid-gen-hd-split-current-config.md) oid。 但是，过量驱动程序应使用 NDIS 在初始化和状态指示过程中提供的信息。

系统管理员可以使用与 OID 第一 \_ 代 \_ 高清 \_ SPLIT \_ \_ 通过 WMI 接口关联的 GUID。 有关标头数据拆分 WMI Guid 的详细信息，请参阅 [对 Header-Data 拆分的 Wmi 支持](wmi-support-for-header-data-split.md)。

NDIS 代表微型端口驱动程序处理 [OID \_ GEN \_ HD \_ SPLIT 的 \_ 当前 \_ 配置](./oid-gen-hd-split-current-config.md) 。 NDIS 基于微型端口驱动程序初始化属性和 [**NDIS \_ 状态 \_ 高清 \_ 拆分 \_ 当前 \_ 配置**](./ndis-status-hd-split-current-config.md) 状态指示，来维护当前的标头数据拆分配置信息。

[**Ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的 **InformationBuffer** 成员包含 [**ndis \_ HD \_ SPLIT \_ 当前 \_ 配置**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_hd_split_current_config)结构。 在 \_ \_ \_ \_ 初始化期间，ndis 还向过量驱动程序提供 ndis HD 拆分当前配置结构，并提供状态指示。

当微型端口驱动程序收到 [OID 第一 \_ 代 \_ hd \_ split \_ 参数](./oid-gen-hd-split-parameters.md) set 请求时，驱动程序必须使用 [**NDIS \_ HD \_ split \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_hd_split_parameters) 结构的内容来更新微型端口适配器的当前配置。 更新后，微型端口驱动程序必须报告其 [**NDIS \_ 状态 \_ 高清 \_ 拆分 \_ 当前 \_ 配置**](./ndis-status-hd-split-current-config.md) 状态指示的更改。 状态指示可确保所有的过量驱动程序都用新信息更新。

当 NDIS 调用 NDIS 6.1 或更高版本协议驱动程序的 [*ProtocolBindAdapterEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex) 函数时，ndis 会提供一个 [**ndis \_ 绑定 \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters) 结构，其中包含指向 [**ndis \_ HD \_ SPLIT \_ 当前 \_ 配置**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_hd_split_current_config) 结构的指针。

当 NDIS 调用 NDIS 6.1 或更高版本的筛选器驱动程序的 [*FilterAttach*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_attach) 函数时，ndis 会提供一个 [**ndis \_ 筛选器 \_ 附加 \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_filter_attach_parameters) 结构，其中包含指向 NDIS \_ HD \_ SPLIT \_ 当前 \_ 配置结构的指针。

 

