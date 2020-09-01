---
title: NDIS 6.80 简介
description: 本部分介绍了 NDIS 6.80，并介绍了 NDIS 6.70 中的更改。 NDIS 6.80 包含在 Windows 10 版本1709中。
ms.assetid: 5E6E12BF-DE34-4CDD-84BB-7708A59134E9
ms.date: 07/05/2017
ms.localizationpriority: medium
ms.openlocfilehash: 65da183716ba7992ba4d32bdbc045a7ea501ddc7
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89206421"
---
# <a name="introduction-to-ndis-680"></a>NDIS 6.80 简介

本主题介绍 (NDIS) 6.80 的网络驱动程序接口规范，并介绍了其主要的设计添加。 NDIS 6.80 包含在 Windows 10 版本1709中。

对于微型端口、协议、筛选器和中间驱动程序，NDIS 6.80 是 NDIS 6.70 的次要版本更新。 有关将 NDIS 1.x 驱动程序移植到 NDIS 6.80 的详细信息，请参阅 [将 ndis 1.x 驱动程序移植到 ndis 6.80](porting-ndis-6-x-drivers-to-ndis-6-70.md)。

对于 NIC 驱动程序，Get-netadapter 类扩展 (NetAdapterCx) 已从版本1.0 更新为 Windows 1709 10 版本1.1 中的版本。

## <a name="feature-updates"></a>功能更新

### <a name="synchronous-oid-requests"></a>同步 OID 请求

NDIS 6.80 为 Oid、同步 OID 请求引入了一项新功能。 与常规 OID 请求相比，同步 OID 调用是低延迟、非阻塞、可伸缩和可靠的。 有关详细信息，请参阅 [NDIS 6.80 中的同步 OID 请求接口](synchronous-oid-request-interface-in-ndis-6-80.md)。

### <a name="rssv2"></a>RSSv2

在 NDIS 6.80 中， [接收方缩放 (rss) ](./receive-side-scaling-version-2-rssv2-.md) 已升级到 rss 版本 2 (RSSv2) 。 RSSv2 通过提供每个 VPort 的传播来改善 RSSv2。 有关详细信息，请参阅 [NDIS 6.80 中的接收方缩放版本 2 (RSSv2) ](receive-side-scaling-version-2-rssv2-in-ndis-6-80.md)。

RSSv2 仅在 Windows 10 版本1709中处于预览阶段。

### <a name="other-new-networking-features"></a>其他新网络功能

NDIS 形成 Windows 上网络驱动程序平台的核心基础。 有关与 NDIS 6.80 同时更新的其他网络驱动程序功能的列表，请参阅 Windows 10 版本1709部分，了解 [驱动程序开发中的新增](../what-s-new-in-driver-development.md)功能。

## <a name="implementing-an-ndis-680-driver"></a>实现 NDIS 6.80 驱动程序

NDIS 6.80 驱动程序必须遵循在 [实现 NDIS 6.30 驱动程序](implementing-an-ndis-6-30-driver.md)中定义的要求。

此外，NDIS 6.80 驱动程序必须符合以下要求：

- 当 ndis 6.80 驱动程序使用 NDIS 注册时，它必须报告正确的 NDIS 版本。

   若要支持 NDIS 6.80，必须在 NDIS_Xxx_DRIVER_CHARACTERISTICS 结构中更新主要和次要 NDIS 版本号。 MajorNdisVersion 成员必须包含6个，并且 MinorNdisVersion 成员必须包含80。 此要求适用于微型端口、协议和筛选器驱动程序。 还必须更新编译器的版本信息 (参阅 [编译 NDIS 6.80 驱动程序](#compiling-an-ndis-680-driver)) 。

## <a name="compiling-an-ndis-680-driver"></a>编译 NDIS 6.80 驱动程序

### <a name="nic-drivers"></a>NIC 驱动程序

有关使用 NetAdapterCx 编译 NIC 驱动程序的详细信息，请参阅 [将 NDIS 微型端口驱动程序移植到 NetAdapterCx (编译设置) ](../netcx/porting-ndis-miniport-drivers-to-netadaptercx.md#compilation-settings)。

### <a name="miniport-protocol-and-filter-drivers"></a>微型端口、协议和筛选器驱动程序

适用于 Windows 10 版本1709的 WDK 支持标头版本控制。 标头版本控制可确保 NDIS 6.80 驱动程序在编译时使用合适的 NDIS 6.80 数据结构。

将以下编译器设置添加到你的驱动程序的 Visual Studio 项目中：

- 对于微型端口驱动程序，请添加 ```NDIS680_MINIPORT=1``` 。
- 对于筛选器或协议驱动程序，请添加 ```NDIS680=1``` 。

有关使用 Windows 10 1709 版的 WDK 构建驱动程序的信息，请参阅 [构建驱动程序](../develop/building-a-driver.md)。

## <a name="api-and-data-structure-changes"></a>API 和数据结构更改

### <a name="new-apis-and-data-structures"></a>新的 Api 和数据结构

以下 Api 和数据结构是在 NDIS 6.80 中新增的。

- [MINIPORT_SYNCHRONOUS_OID_REQUEST](/windows-hardware/drivers/ddi/ndis/nf-ndis-miniport_synchronous_oid_request)
- [FILTER_SYNCHRONOUS_OID_REQUEST](/windows-hardware/drivers/ddi/ndis/nf-ndis-filter_synchronous_oid_request)
- [FILTER_SYNCHRONOUS_OID_REQUEST_COMPLETE](/windows-hardware/drivers/ddi/ndis/nf-ndis-filter_synchronous_oid_request_complete)
- [NdisFSynchronousOidRequest](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfsynchronousoidrequest)
- [NdisSynchronousOidRequest](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissynchronousoidrequest)
- [OID_GEN_RECEIVE_SCALE_PARAMETERS_V2](oid-gen-receive-scale-parameters-v2.md)
- [OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES](oid-gen-rss-set-indirection-table-entries.md)
- [NDIS_RECEIVE_SCALE_PARAMETERS_V2](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_scale_parameters_v2)
- [NDIS_RSS_SET_INDIRECTION_ENTRIES](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_rss_set_indirection_entries)
- [NDIS_RSS_SET_INDIRECTION_ENTRY](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_rss_set_indirection_entry)

### <a name="updated-apis-and-data-structures"></a>更新的 Api 和数据结构

以下 Api 和数据结构已在 NDIS 6.80 中更新。

- [NDIS_MINIPORT_DRIVER_CHARACTERISTICS](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_driver_characteristics)
- [NDIS_FILTER_DRIVER_CHARACTERISTICS](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_filter_driver_characteristics)
- [NDIS_RECEIVE_SCALE_CAPABILITIES](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_scale_capabilities)