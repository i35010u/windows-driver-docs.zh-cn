---
title: GUID_NDIS_GEN_STATISTICS
description: 本主题描述了 NDIS WMI 接口的 GUID_NDIS_GEN_STATISTICS GUID。
ms.assetid: 3751d4e7-7991-4329-9eb2-6a44ca1190d4
keywords:
- GUID_NDIS_GEN_STATISTICS，WDK GUID_NDIS_GEN_STATISTICS 网络驱动程序
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: b1d0e8e0e795d7f0fde612a8de4d5e9701f43c56
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89218107"
---
# <a name="guid_ndis_gen_statistics"></a>GUID_NDIS_GEN_STATISTICS

WMI 客户端可以使用 GUID_NDIS_GEN_STATISTICS 方法 GUID 来获取微型端口适配器统计信息。 在 NDIS 6.0 和更高版本中支持此 WMI GUID。

当 WMI 客户端发出 GUID_NDIS_GEN_STATISTICS WMI 方法请求时，NDIS 将返回微型端口适配器或 NDIS 端口的当前统计信息。 应 NDIS_WMI_DEFAULT_METHOD_ID WMI 方法标识符，WMI 输入缓冲区应包含 [NDIS_WMI_METHOD_HEADER](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_wmi_method_header) 的结构。

NDIS 使用 [OID_GEN_STATISTICS](oid-gen-statistics.md) OID 来获取微型端口适配器的统计信息。 此 OID 对于支持 NDIS 6.0 和更高版本的微型端口驱动程序是必需的。 统计信息计数器是未签名的64位值。 微型端口驱动程序以 NDIS_STATISTICS_INFO 结构返回统计信息。

NDIS 随 GUID 返回的数据缓冲区包含 NDIS_STATISTICS_INFO 结构。