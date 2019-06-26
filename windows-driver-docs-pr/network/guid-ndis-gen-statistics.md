---
title: GUID_NDIS_GEN_STATISTICS
description: 本主题介绍 NDIS WMI 接口的 GUID_NDIS_GEN_STATISTICS GUID。
ms.assetid: 3751d4e7-7991-4329-9eb2-6a44ca1190d4
keywords:
- GUID_NDIS_GEN_STATISTICS，WDK GUID_NDIS_GEN_STATISTICS 网络驱动程序
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8e762230f007223f8fc40efb30307c30739a5a30
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382698"
---
# <a name="guidndisgenstatistics"></a>GUID_NDIS_GEN_STATISTICS

WMI 客户端可以使用 GUID_NDIS_GEN_STATISTICS 方法 GUID 获取微型端口适配器的统计信息。 NDIS 6.0 及更高版本支持此 WMI GUID。

如果 WMI 客户端发出 GUID_NDIS_GEN_STATISTICS WMI 方法请求时，NDIS 返回微型端口适配器或 NDIS 端口的当前统计信息。 WMI 方法标识符应 NDIS_WMI_DEFAULT_METHOD_ID，且应包含 WMI 输入的缓冲区[NDIS_WMI_METHOD_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_wmi_method_header)结构。

使用 NDIS [OID_GEN_STATISTICS](oid-gen-statistics.md) OID，若要获取的微型端口适配器统计信息。 此 OID 是必需的支持 NDIS 6.0 及更高版本的微型端口驱动程序。 统计信息计数器是无符号的 64 位值。 微型端口驱动程序返回 NDIS_STATISTICS_INFO 结构中的统计信息。

NDIS 返回 GUID 的数据缓冲区包含 NDIS_STATISTICS_INFO 结构。

