---
title: GUID_NDIS_GEN_LINK_PARAMETERS
description: 本主题描述了 NDIS WMI 接口的 GUID_NDIS_GEN_LINK_PARAMETERS GUID。
keywords:
- GUID_NDIS_GEN_LINK_PARAMETERS，WDK GUID_NDIS_GEN_LINK_PARAMETERS 网络驱动程序
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5df2995caaea7513d0bbc9b80c43258f469d737b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786169"
---
# <a name="guid_ndis_gen_link_parameters"></a>GUID_NDIS_GEN_LINK_PARAMETERS

WMI 客户端可以使用 GUID_NDIS_GEN_LINK_PARAMETERS 设置 GUID 来设置微型端口适配器的链接参数。 在 NDIS 6.0 和更高版本中支持此 WMI GUID。

NDIS 将此 GUID 转换为 [OID_GEN_LINK_PARAMETERS](oid-gen-link-parameters.md) OID，以设置微型端口适配器的当前链接参数。 此 OID 对于支持 NDIS 6.0 和更高版本的微型端口驱动程序是必需的。

WMI 输入缓冲区指定 NDIS 应该设置的数据。 输入缓冲区包含后跟[NDIS_LINK_PARAMETERS](./oid-gen-link-parameters.md)结构的[NDIS_WMI_SET_HEADER](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_wmi_set_header)结构。
