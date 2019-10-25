---
title: GUID_NDIS_GEN_LINK_PARAMETERS
description: 本主题描述了 NDIS WMI 接口的 GUID_NDIS_GEN_LINK_PARAMETERS GUID。
ms.assetid: 83895adf-2e66-4820-8037-52eb352b82fc
keywords:
- GUID_NDIS_GEN_LINK_PARAMETERS，WDK GUID_NDIS_GEN_LINK_PARAMETERS 网络驱动程序
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 386d57b310ea340e582a1dcb2f87221e878589d9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842291"
---
# <a name="guid_ndis_gen_link_parameters"></a>GUID_NDIS_GEN_LINK_PARAMETERS

WMI 客户端可以使用 GUID_NDIS_GEN_LINK_PARAMETERS set GUID 来设置微型端口适配器的链接参数。 在 NDIS 6.0 和更高版本中支持此 WMI GUID。

NDIS 将此 GUID 转换为[OID_GEN_LINK_PARAMETERS](oid-gen-link-parameters.md) OID，以设置微型端口适配器的当前链接参数。 此 OID 对于支持 NDIS 6.0 和更高版本的微型端口驱动程序是必需的。

WMI 输入缓冲区指定 NDIS 应该设置的数据。 输入缓冲区包含后跟[NDIS_LINK_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-link-parameters)结构的[NDIS_WMI_SET_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_wmi_set_header)结构。

