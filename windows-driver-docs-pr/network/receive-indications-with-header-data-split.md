---
title: 标头数据拆分的接收指示
description: 标头数据拆分的接收指示
ms.assetid: 76abeac8-ca6e-40b1-a46e-83ae90d9192e
keywords:
- 标头-数据拆分 WDK，接收指示
- 收到的数据格式 WDK 标头-数据拆分
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2e9fdcba79c33acbd4a08db85e058d0d96f6f915
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844861"
---
# <a name="receive-indications-with-header-data-split"></a>标头数据拆分的接收指示





支持标头-数据拆分的微型端口驱动程序必须以标头-数据拆分所需的格式指示收到的数据。 例如，标头缓冲区应在一个连续的存储块中，而数据缓冲区必须包含回填空间。

拆分框架中的标头信息决不能包括虚拟 LAN （VLAN）标记。 标头-数据拆分要求在硬件中支持 VLAN，并需要从传入帧中删除 VLAN 标记，并将其放入[**NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构中的**Ieee8021QNetBufferListInfo** OOB 信息。 微型端口驱动程序必须在[**NDIS\_微型端口\_适配器**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)的**MacOptions**成员中指定对 VLAN 的支持\_常规\_属性结构和响应[OID\_代\_MAC\_选项](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-mac-options)OID 查询。

NDIS 和过量驱动程序或用户模式应用程序使用[OID\_GEN\_HD\_拆分\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-hd-split-parameters)OID 以设置微型端口适配器的当前标头-数据拆分设置。 如果 NDIS\_HD\_SPLIT\_将 Ndis 的**HDSplitCombineFlags**成员中\_所有\_标头标志合并\_[**HD\_SPLIT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_hd_split_parameters)\_，微型端口适配器必须合并所有拆分框架。 如果在硬件中启用了标头-数据拆分，则微型端口驱动程序必须先将标头和数据合并，然后再将帧指示到 NDIS。 有关 OID\_GEN\_HD\_拆分\_参数和其他管理和配置问题的详细信息，请参阅[标头-数据拆分管理和配置](header-data-split-administration-and-configuration.md)。

本部分包括：

[分配标头缓冲区](allocating-the-header-buffer.md)

[为数据缓冲区分配回填](allocating-backfill-for-the-data-buffer.md)

[设置 NET\_缓冲区\_列表信息](setting-net-buffer-list-information.md)

 

 





