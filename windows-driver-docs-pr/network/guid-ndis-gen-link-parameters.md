---
title: GUID_NDIS_GEN_LINK_PARAMETERS
description: 本主题描述了 NDIS WMI 接口的 GUID_NDIS_GEN_LINK_PARAMETERS GUID。
ms.assetid: 83895adf-2e66-4820-8037-52eb352b82fc
keywords:
- GUID_NDIS_GEN_LINK_PARAMETERS，WDK GUID_NDIS_GEN_LINK_PARAMETERS 网络驱动程序
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c159dd79119f5a43635968df4f3cff852f8614b
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89207561"
---
# <a name="guid_ndis_gen_link_parameters"></a>GUID_NDIS_GEN_LINK_PARAMETERS

WMI 客户端可以使用 GUID_NDIS_GEN_LINK_PARAMETERS 设置 GUID 来设置微型端口适配器的链接参数。 在 NDIS 6.0 和更高版本中支持此 WMI GUID。

NDIS 将此 GUID 转换为 [OID_GEN_LINK_PARAMETERS](oid-gen-link-parameters.md) OID，以设置微型端口适配器的当前链接参数。 此 OID 对于支持 NDIS 6.0 和更高版本的微型端口驱动程序是必需的。

WMI 输入缓冲区指定 NDIS 应该设置的数据。 输入缓冲区包含后跟[NDIS_LINK_PARAMETERS](./oid-gen-link-parameters.md)结构的[NDIS_WMI_SET_HEADER](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_wmi_set_header)结构。