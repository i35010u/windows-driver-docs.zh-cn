---
title: NDIS 6.50 简介
description: 本部分介绍 NDIS 6.50，并介绍了从 NDIS 6.40 的更改。 NDIS 6.50 包含在 Windows 10 版本 1507年和更高版本。
ms.assetid: 8D2EA09D-3FA3-467B-861A-AA15C790FCD3
ms.date: 06/01/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8aa3f2540e29fdca19a816387f37a5ed02ae781a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547231"
---
# <a name="introduction-to-ndis-650"></a>NDIS 6.50 简介

本主题介绍网络驱动程序接口规范 (NDIS) 6.50 并描述其主要设计新增功能。 NDIS 6.50 包含在 Windows 10 版本 1507年和更高版本。

NDIS 6.50 是次要版本更新到 NDIS 6.40。 有关移植到 NDIS 6.50 NDIS 6.x 驱动程序的详细信息，请参阅[移植 NDIS 6.x 驱动程序到 NDIS 6.50](porting-ndis-6-x-drivers-to-ndis-6-50.md)。

## <a name="feature-updates"></a>功能更新

NDIS 6.50 NDIS 6.40 的增量更新，并且不包含任何主要的新功能。

## <a name="implementing-an-ndis-650-driver"></a>实现 NDIS 6.50 驱动程序

NDIS 6.50 驱动程序必须遵循在中定义的要求[实现的 NDIS 6.30 驱动程序](implementing-an-ndis-6-30-driver.md)。

此外，NDIS 6.50 驱动程序必须符合以下要求：

- NDIS 6.50 驱动程序必须报告正确的 NDIS 版本时它会向 NDIS 注册。
   
   您必须更新的主版本号和次 NDIS 版本编号 NDIS_Xxx_DRIVER_CHARACTERISTICS 结构中以支持 NDIS 6.50。 MajorNdisVersion 成员必须包含 6 和 MinorNdisVersion 成员必须包含 50。 此要求适用于微型端口、 协议和筛选器驱动程序。 您还必须更新编译器的版本信息 (请参阅[编译的 NDIS 6.50 驱动程序](#compiling-an-ndis-650-driver))。

- NDIS 6.50 微型端口驱动程序适用于 Windows 10 版本 1507年和更高版本必须使用数据结构的 NDIS 6.50 版本。 有关详细信息，请参阅[使用 NDIS 6.50 数据结构](#using-ndis-650-data-structures)。

## <a name="compiling-an-ndis-650-driver"></a>编译 NDIS 6.50 驱动程序

WDK 适用于 Windows 10 版本 1507年支持标头版本控制。 标头版本控制可确保 NDIS 6.50 驱动程序在编译时使用的合适的 NDIS 6.50 数据结构。

将以下编译器设置添加到您的驱动程序的 Visual Studio 项目：

- 微型端口驱动程序，添加```NDIS650_MINIPORT=1```。
- 筛选器或协议驱动程序添加```NDIS650=1```。

了解生成的驱动程序有 Windows 10 版本 1507年版本的 WDK 中，请参阅[构建一个驱动程序](../develop/building-a-driver.md)。

## <a name="using-ndis-650-data-structures"></a>使用 NDIS 6.50 数据结构

### <a name="new-data-structures"></a>新的数据结构

以下数据结构是 NDIS 6.50 中的新增功能。

- [OID_WWAN_SYS_CAPS](https://msdn.microsoft.com/library/windows/hardware/mt799833)
- [OID_WWAN_DEVICE_CAPS_EX](https://msdn.microsoft.com/library/windows/hardware/mt799830)
- [OID_WWAN_SLOT_INFO_STATUS](https://msdn.microsoft.com/library/windows/hardware/mt799832)
- [OID_WWAN_NETWORK_IDLE_HINT](https://msdn.microsoft.com/library/windows/hardware/dn931089) 
- [NDIS_STATUS_PD_CURRENT_CONFIG](https://msdn.microsoft.com/library/windows/hardware/dn931850)
- [NDIS_PD_CAPABILITIES](https://msdn.microsoft.com/library/windows/hardware/dn931833)
- [NDIS_PD_CLOSE_PROVIDER_PARAMETERS](https://msdn.microsoft.com/library/windows/hardware/dn931834)
- [NDIS_PD_CONFIG](https://msdn.microsoft.com/library/windows/hardware/dn931835)
- [NDIS_PD_COUNTER_PARAMETERS](https://msdn.microsoft.com/library/windows/hardware/dn931836)
- [NDIS_PD_COUNTER_VALUE](https://msdn.microsoft.com/library/windows/hardware/dn931838)
- [NDIS_PD_FILTER_COUNTER](https://msdn.microsoft.com/library/windows/hardware/dn931839)
- [NDIS_PD_FILTER_PARAMETERS](https://msdn.microsoft.com/library/windows/hardware/dn931840)
- [NDIS_PD_ON_RSS_QUEUE_PARAMETERS](https://msdn.microsoft.com/library/windows/hardware/dn931841)
- [NDIS_PD_OPEN_PROVIDER_PARAMETERS](https://msdn.microsoft.com/library/windows/hardware/dn931842)
- [NDIS_PD_PROVIDER_DISPATCH](https://msdn.microsoft.com/library/windows/hardware/dn931843)
- [NDIS_PD_QUEUE](https://msdn.microsoft.com/library/windows/hardware/dn931844)
- [NDIS_PD_QUEUE_DISPATCH](https://msdn.microsoft.com/library/windows/hardware/dn931845)
- [NDIS_PD_QUEUE_PARAMETERS](https://msdn.microsoft.com/library/windows/hardware/dn931846)
- [NDIS_PD_RECEIVE_QUEUE_COUNTER](https://msdn.microsoft.com/library/windows/hardware/dn931848)
- [NDIS_PD_TRANSMIT_QUEUE_COUNTER](https://msdn.microsoft.com/library/windows/hardware/dn931849)
- [PD_BUFFER](https://msdn.microsoft.com/library/windows/hardware/dn931863)
- [PD_BUFFER_8021Q_INFO](https://msdn.microsoft.com/library/windows/hardware/dn931864)
- [PD_BUFFER_VIRTUAL_SUBNET_INFO](https://msdn.microsoft.com/library/windows/hardware/dn931865)

### <a name="updated-data-structures"></a>更新后的数据结构

在 NDIS 6.50 中更新了以下数据结构。

- [NET_PNP_EVENT_NOTIFICATION](https://msdn.microsoft.com/library/windows/hardware/ff568752)
- [NDIS_OID_REQUEST](https://msdn.microsoft.com/library/windows/hardware/ff566710)
- [NDIS_NET_BUFFER_LIST_INFO](https://msdn.microsoft.com/library/windows/hardware/ff566569)
- [NdisMGetDeviceProperty](https://msdn.microsoft.com/library/windows/hardware/ff563592)
- [NDIS_SWITCH_OPTIONAL_HANDLERS](https://msdn.microsoft.com/library/windows/hardware/hh598219)
- [NDIS_SWITCH_NIC_SAVE_STATE](https://msdn.microsoft.com/library/windows/hardware/hh598216)

## <a name="ndis-651"></a>NDIS 6.51

NDIS 6.51 是非常次要版本更新到 NDIS 6.50。 NDIS 6.51 包含在 Windows 10，版本 1511年及更高版本。 NDIS 6.50 的所有信息也都适用于 NDIS 6.51 有以下例外：

- MinorNdisVersion 更改从 50 到 51 个向 NDIS 注册您的驱动程序时。
- 编译器设置更改从```NDIS650_MINIPORT=1```微型端口驱动程序和```NDIS650=1```筛选器或协议驱动程序，请向```NDIS651_MINIPORT=1```和```NDIS651=1```分别。

