---
title: 标头数据拆分的接收指示
description: 标头数据拆分的接收指示
keywords:
- 标头-数据拆分 WDK，接收指示
- 收到的数据格式 WDK 标头-数据拆分
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4c321cc690bdfb9ad55b982713708062971dbc44
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839443"
---
# <a name="receive-indications-with-header-data-split"></a>标头数据拆分的接收指示





支持标头-数据拆分的微型端口驱动程序必须以标头-数据拆分所需的格式指示收到的数据。 例如，标头缓冲区应在一个连续的存储块中，而数据缓冲区必须包含回填空间。

拆分框架中的标头信息决不能包括虚拟 LAN (VLAN) 标记。 标头-数据拆分要求在硬件中支持 VLAN，并需要从传入帧中删除 VLAN 标记，并将其放入 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构中的 **Ieee8021QNetBufferListInfo** OOB 信息。 微型端口驱动程序必须在 [**NDIS \_ 微型端口 \_ 适配器 \_ 常规 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)结构的 **MacOptions** 成员中指定对 VLAN 的支持，并为响应 [oid \_ GEN \_ MAC \_ OPTIONS](./oid-gen-mac-options.md) OID 查询。

NDIS 和过量驱动程序或用户模式应用程序使用 [oid \_ GEN \_ HD \_ SPLIT \_ PARAMETERS](./oid-gen-hd-split-parameters.md) oid 设置微型端口适配器的当前标头-数据拆分设置。 如果设置了 \_ \_ \_ \_ \_ [**Ndis \_ hd \_ SPLIT \_ PARAMETERS**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_hd_split_parameters)结构的 **HDSplitCombineFlags** 成员中的 ndis HD split "合并所有标头" 标志，则微型端口适配器必须合并所有拆分框架。 如果在硬件中启用了标头-数据拆分，则微型端口驱动程序必须先将标头和数据合并，然后再将帧指示到 NDIS。 有关 OID \_ GEN \_ HD \_ SPLIT \_ 参数和其他管理和配置问题的详细信息，请参阅 [标头-数据拆分管理和配置](setting-the-current-header-data-split-configuration.md)。

本节包括：

[分配标头缓冲区](allocating-the-header-buffer.md)

[为数据缓冲区分配回填](allocating-backfill-for-the-data-buffer.md)

[设置网络 \_ 缓冲区 \_ 列表信息](setting-net-buffer-list-information.md)

 

