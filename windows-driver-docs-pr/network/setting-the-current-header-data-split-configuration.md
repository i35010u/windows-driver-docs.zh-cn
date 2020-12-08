---
title: 设置当前的标头数据拆分配置
description: 设置当前的标头数据拆分配置
keywords:
- 标头-数据拆分 WDK，配置
- 当前标头-数据拆分配置 WDK 网络
- 状态信息 WDK 标头-数据拆分
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe3802f60c60b6b7639c9085671273379265b1f1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96790471"
---
# <a name="setting-the-current-header-data-split-configuration"></a>设置当前的标头数据拆分配置





NDIS 和过量驱动程序或用户模式应用程序使用 [oid \_ GEN \_ HD \_ SPLIT \_ PARAMETERS](./oid-gen-hd-split-parameters.md) oid 设置微型端口适配器的当前标头-数据拆分设置。 提供标头数据拆分服务的 NDIS 6.1 和更高的微型端口驱动程序必须支持此 OID。 否则，此 OID 是可选的。

系统管理员可以通过 WMI 接口使用与此 OID 关联的 GUID。 有关标头数据拆分 WMI Guid 的详细信息，请参阅 [对 Header-Data 拆分的 Wmi 支持](wmi-support-for-header-data-split.md)。

[**Ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的 **InformationBuffer** 成员包含 [**ndis \_ HD \_ SPLIT \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_hd_split_parameters)结构。

如果设置了 \_ \_ \_ \_ \_ Ndis hd split 参数的 **HDSplitCombineFlags** 成员中的 ndis HD split 合并所有标头标志 \_ \_ \_ ，则微型端口适配器必须合并所有拆分框架。 如果在硬件中启用了标头数据拆分，则微型端口驱动程序必须在驱动程序指示帧到 NDIS 之前合并标头和数据。

例如，在 NDIS 5 时，NDIS 可以使用 OID \_ \_ \_ 第一代 HD split \_ PARAMETERS oid 设置 ndis \_ HD \_ split \_ 组合 \_ ALL \_ 标头标志。*x* 协议驱动程序绑定到 NDIS 6.1 微型端口适配器。 在将 OID 传递到微型端口驱动程序并更新微型端口适配器的 **\* HeaderDataSplit** 标准化关键字（如果需要）之前，NDIS 会处理此 oid。 如果禁用了标头-数据拆分，NDIS 不会将此 OID 发送到微型端口适配器。

 

