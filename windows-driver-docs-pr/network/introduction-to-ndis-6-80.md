---
title: NDIS 6.80 简介
description: 本部分介绍 NDIS 6.80，并介绍了从 NDIS 6.70 的更改。 NDIS 6.80 包含在 Windows 10，版本 1709年。
ms.assetid: 5E6E12BF-DE34-4CDD-84BB-7708A59134E9
ms.date: 07/05/2017
ms.localizationpriority: medium
ms.openlocfilehash: 210f5f2bc0a7f1de558b15bbb662d66bacd01c16
ms.sourcegitcommit: 0504cc497918ebb7b41a205f352046a66c0e26a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/08/2019
ms.locfileid: "65405226"
---
# <a name="introduction-to-ndis-680"></a>NDIS 6.80 简介

本主题介绍网络驱动程序接口规范 (NDIS) 6.80 并描述其主要设计新增功能。 NDIS 6.80 包含在 Windows 10，版本 1709年。

NDIS 6.80 是次要版本更新到 NDIS 6.70 微型端口、 协议、 筛选器和中间驱动程序。 有关移植到 NDIS 6.80 NDIS 6.x 驱动程序的详细信息，请参阅[移植 NDIS 6.x 驱动程序到 NDIS 6.80](porting-ndis-6-x-drivers-to-ndis-6-70.md)。

NIC 驱动程序，请 NetAdapter 类扩展 (NetAdapterCx) 已更新从版本 1.0 到版本 1.1 中 Windows 10 版本 1709年。

## <a name="feature-updates"></a>功能更新

### <a name="synchronous-oid-requests"></a>OID 的同步请求

NDIS 6.80 的 Oid 引入了新功能，请求同步 OID。 OID 的同步调用是低延迟非阻止性、 可缩放和可靠相比常规 OID 请求。 有关详细信息，请参阅[同步 OID 请求接口在 NDIS 6.80](synchronous-oid-request-interface-in-ndis-6-80.md)。

### <a name="rssv2"></a>RSSv2

在 NDIS 6.80[接收方缩放 (RSS)](ndis-receive-side-scaling2.md)已升级到 RSS 版本 2 (RSSv2)。 通过提供每个 VPort 分布 RSSv2 提升 RSSv2。 有关详细信息，请参阅[接收端缩放版本 2 (RSSv2) 在 NDIS 6.80](receive-side-scaling-version-2-rssv2-in-ndis-6-80.md)。

RSSv2 为预览版，仅在 Windows 10 版本 1709年中。

### <a name="other-new-networking-features"></a>其他新的网络功能

NDIS 窗体上 Windows 的网络驱动程序平台的核心基础。 在 NDIS 6.80 在同一时间更新其他网络驱动程序功能的列表，请参阅 Windows 10 版本 1709年上的网络部分[什么是驱动程序开发中的新增功能](../what-s-new-in-driver-development.md)。

## <a name="implementing-an-ndis-680-driver"></a>实现 NDIS 6.80 驱动程序

NDIS 6.80 驱动程序必须遵循在中定义的要求[实现的 NDIS 6.30 驱动程序](implementing-an-ndis-6-30-driver.md)。

此外，NDIS 6.80 驱动程序必须符合以下要求：

- NDIS 6.80 驱动程序必须报告正确的 NDIS 版本时它会向 NDIS 注册。

   您必须更新的主版本号和次 NDIS 版本编号 NDIS_Xxx_DRIVER_CHARACTERISTICS 结构中以支持 NDIS 6.80。 MajorNdisVersion 成员必须包含 6 和 MinorNdisVersion 成员必须包含 80。 此要求可适用于微型端口、 协议和筛选器驱动程序。 您还必须更新编译器的版本信息 (请参阅[编译的 NDIS 6.80 驱动程序](#compiling-an-ndis-680-driver))。

## <a name="compiling-an-ndis-680-driver"></a>编译 NDIS 6.80 驱动程序

### <a name="nic-drivers"></a>NIC 驱动程序

有关编译 NetAdapterCx NIC 驱动程序的详细信息，请参阅[NetAdapterCx （编译设置） 移植 NDIS 微型端口驱动程序](../netcx/porting-ndis-miniport-drivers-to-netadaptercx.md#compilation-settings)。

### <a name="miniport-protocol-and-filter-drivers"></a>微型端口、 协议和筛选器驱动程序

WDK 适用于 Windows 10 1709年版支持标头版本控制。 标头版本控制可确保 NDIS 6.80 驱动程序在编译时使用的合适的 NDIS 6.80 数据结构。

将以下编译器设置添加到您的驱动程序的 Visual Studio 项目：

- 微型端口驱动程序，添加```NDIS680_MINIPORT=1```。
- 筛选器或协议驱动程序添加```NDIS680=1```。

有关构建与 Windows 10，版本 1709年版本的 WDK，驱动程序的信息，请参阅[构建一个驱动程序](../develop/building-a-driver.md)。

## <a name="api-and-data-structure-changes"></a>API 和数据结构更改

### <a name="new-apis-and-data-structures"></a>新的 Api 和数据结构

以下 Api 和数据结构是 NDIS 6.80 中的新增功能。

- [MINIPORT_SYNCHRONOUS_OID_REQUEST](https://msdn.microsoft.com/library/windows/hardware/0DDF9CF8-91F6-4D7C-A8E8-FC425BF155CB)
- [FILTER_SYNCHRONOUS_OID_REQUEST](https://msdn.microsoft.com/library/windows/hardware/AC84B27B-6FBF-429D-A8FA-F3C8F583F738)
- [FILTER_SYNCHRONOUS_OID_REQUEST_COMPLETE](https://msdn.microsoft.com/library/windows/hardware/E0749F52-CC7C-484D-8350-1986154957C1)
- [NdisFSynchronousOidRequest](https://msdn.microsoft.com/library/windows/hardware/01B625EB-AB6D-496F-95F2-22845460324A)
- [NdisSynchronousOidRequest](https://msdn.microsoft.com/library/windows/hardware/BF539DDA-59ED-4010-88BC-3C7D8DC475EF)
- [OID_GEN_RECEIVE_SCALE_PARAMETERS_V2](oid-gen-receive-scale-parameters-v2.md)
- [OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES](oid-gen-rss-set-indirection-table-entries.md)
- [NDIS_RECEIVE_SCALE_PARAMETERS_V2](https://msdn.microsoft.com/library/windows/hardware/96EAB6EE-BF9A-46AD-8DED-5D9BD2B6F219)
- [NDIS_RSS_SET_INDIRECTION_ENTRIES](https://msdn.microsoft.com/library/windows/hardware/9AB69EC6-FE78-4242-89C7-D36AA16676BF)
- [NDIS_RSS_SET_INDIRECTION_ENTRY](https://msdn.microsoft.com/library/windows/hardware/4430E19F-C603-4C52-8FC8-C36197FD2996)

### <a name="updated-apis-and-data-structures"></a>已更新的 Api 和数据结构

在 NDIS 6.80 中更新了以下 Api 和数据结构。

- [NDIS_MINIPORT_DRIVER_CHARACTERISTICS](https://msdn.microsoft.com/library/windows/hardware/ff565958)
- [NDIS_FILTER_DRIVER_CHARACTERISTICS](https://msdn.microsoft.com/library/windows/hardware/ff565515)
- [NDIS_RECEIVE_SCALE_CAPABILITIES](https://msdn.microsoft.com/library/windows/hardware/ff567220)

