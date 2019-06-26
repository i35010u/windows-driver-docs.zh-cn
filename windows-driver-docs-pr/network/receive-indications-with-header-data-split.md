---
title: 标头数据拆分的接收指示
description: 标头数据拆分的接收指示
ms.assetid: 76abeac8-ca6e-40b1-a46e-83ae90d9192e
keywords:
- 标头数据拆分 WDK，接收指示
- 接收到的数据格式 WDK 标头数据拆分
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e4c7f424021058b395e7a51a0d2f9a2aefe71dd7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368475"
---
# <a name="receive-indications-with-header-data-split"></a>标头数据拆分的接收指示





标头数据拆分格式支持标头数据拆分必须指示接收到的数据的微型端口驱动程序要求。 例如，标头缓冲区都应在存储的连续块和数据缓冲区必须包括回填的空间。

拆分帧中的标头信息必须永远不会包括虚拟 LAN (VLAN) 标记。 标头数据拆分 VLAN 在硬件中需要支持，并且需要从传入的帧中删除 VLAN 标记并将它们中放置**Ieee8021QNetBufferListInfo** OOB 中的信息[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构。 微型端口驱动程序必须指定支持在 VLAN **MacOptions**的成员[ **NDIS\_微型端口\_适配器\_常规\_属性** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)结构以及在响应[OID\_常规\_MAC\_选项](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-mac-options)OID 查询。

NDIS 和基础驱动程序或用户模式应用程序使用[OID\_代\_HD\_拆分\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-hd-split-parameters)OID，设置当前标头数据拆分微型端口适配器的设置。 如果 NDIS\_HD\_拆分\_合并\_所有\_标头标志中**HDSplitCombineFlags**隶属[ **NDIS\_HD\_拆分\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_hd_split_parameters)设置结构、 微型端口适配器必须将所有拆分帧结合都起来。 如果硬件中启用了标头数据拆分，微型端口驱动程序必须先组合的标头和数据之前，该值指示到 NDIS 帧。 有关 OID 的详细信息\_GEN\_HD\_拆分\_参数和其他管理和配置的问题，请参阅[标头数据拆分管理和配置](header-data-split-administration-and-configuration.md).

本部分包括：

[分配标头缓冲区](allocating-the-header-buffer.md)

[为数据缓冲区分配回填](allocating-backfill-for-the-data-buffer.md)

[设置 NET\_缓冲区\_列出信息](setting-net-buffer-list-information.md)

 

 





