---
title: 设置当前的标头数据拆分配置
description: 设置当前的标头数据拆分配置
ms.assetid: b5b20ce8-1522-4729-8d0a-bc2d2c5afff2
keywords:
- 标头-数据拆分 WDK，配置
- 当前标头-数据拆分配置 WDK 网络
- 状态信息 WDK 标头-数据拆分
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3df77ac3693a61a508eae1adfc730c5e7af901ed
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841935"
---
# <a name="setting-the-current-header-data-split-configuration"></a>设置当前的标头数据拆分配置





NDIS 和过量驱动程序或用户模式应用程序使用[OID\_GEN\_HD\_拆分\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-hd-split-parameters)OID 以设置微型端口适配器的当前标头-数据拆分设置。 提供标头数据拆分服务的 NDIS 6.1 和更高的微型端口驱动程序必须支持此 OID。 否则，此 OID 是可选的。

系统管理员可以通过 WMI 接口使用与此 OID 关联的 GUID。 有关标头数据拆分 WMI Guid 的详细信息，请参阅[对标头数据拆分的 WMI 支持](wmi-support-for-header-data-split.md)。

[ **\_OID 的 ndis\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含[**ndis\_HD\_SPLIT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_hd_split_parameters)结构。

如果 NDIS\_HD\_SPLIT\_将 NDIS 的**HDSplitCombineFlags**成员中\_所有\_标头标志合并\_HD\_已设置了 "拆分\_参数"，则微型端口适配器必须合并所有拆分框架。 如果在硬件中启用了标头数据拆分，则微型端口驱动程序必须在驱动程序指示帧到 NDIS 之前合并标头和数据。

例如，NDIS 可能会使用 OID\_GEN\_HD\_拆分\_参数 OID，将 NDIS 设置\_HD\_SPLIT\_在 NDIS 5 时合并\_所有\_标头标志。*x*协议驱动程序绑定到 NDIS 6.1 微型端口适配器。 在将 OID 传递到微型端口驱动程序之前，NDIS 会处理此 OID，并根据需要更新微型端口适配器的 **\*HeaderDataSplit**标准化关键字。 如果禁用了标头-数据拆分，NDIS 不会将此 OID 发送到微型端口适配器。

 

 





