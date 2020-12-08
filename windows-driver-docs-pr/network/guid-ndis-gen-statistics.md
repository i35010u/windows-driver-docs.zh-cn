---
title: GUID_NDIS_GEN_STATISTICS
description: 本主题描述了 NDIS WMI 接口的 GUID_NDIS_GEN_STATISTICS GUID。
keywords:
- GUID_NDIS_GEN_STATISTICS，WDK GUID_NDIS_GEN_STATISTICS 网络驱动程序
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: cee62aa146f3d4adbc166473facd15e0760f2fe4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822921"
---
# <a name="guid_ndis_gen_statistics"></a>GUID_NDIS_GEN_STATISTICS

WMI 客户端可以使用 GUID_NDIS_GEN_STATISTICS 方法 GUID 来获取微型端口适配器统计信息。 在 NDIS 6.0 和更高版本中支持此 WMI GUID。

当 WMI 客户端发出 GUID_NDIS_GEN_STATISTICS WMI 方法请求时，NDIS 将返回微型端口适配器或 NDIS 端口的当前统计信息。 应 NDIS_WMI_DEFAULT_METHOD_ID WMI 方法标识符，WMI 输入缓冲区应包含 [NDIS_WMI_METHOD_HEADER](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_wmi_method_header) 的结构。

NDIS 使用 [OID_GEN_STATISTICS](oid-gen-statistics.md) OID 来获取微型端口适配器的统计信息。 此 OID 对于支持 NDIS 6.0 和更高版本的微型端口驱动程序是必需的。 统计信息计数器是未签名的64位值。 微型端口驱动程序以 NDIS_STATISTICS_INFO 结构返回统计信息。

NDIS 随 GUID 返回的数据缓冲区包含 NDIS_STATISTICS_INFO 结构。
