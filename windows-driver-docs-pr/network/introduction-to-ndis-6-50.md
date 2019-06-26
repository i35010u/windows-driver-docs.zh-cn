---
title: NDIS 6.50 简介
description: 本部分介绍 NDIS 6.50，并介绍了从 NDIS 6.40 的更改。 NDIS 6.50 包含在 Windows 10 版本 1507年和更高版本。
ms.assetid: 8D2EA09D-3FA3-467B-861A-AA15C790FCD3
ms.date: 06/01/2017
ms.localizationpriority: medium
ms.openlocfilehash: 28e164df3212d946bad447722e838a4dd0a5e290
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386348"
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

- [OID_WWAN_SYS_CAPS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-sys-caps)
- [OID_WWAN_DEVICE_CAPS_EX](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-device-caps-ex)
- [OID_WWAN_SLOT_INFO_STATUS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-slot-info-status)
- [OID_WWAN_NETWORK_IDLE_HINT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-network-idle-hint) 
- [NDIS_STATUS_PD_CURRENT_CONFIG](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pd-current-config)
- [NDIS_PD_CAPABILITIES](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pd_capabilities)
- [NDIS_PD_CLOSE_PROVIDER_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_pd_close_provider_parameters)
- [NDIS_PD_CONFIG](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pd_config)
- [NDIS_PD_COUNTER_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_pd_counter_parameters)
- [NDIS_PD_COUNTER_VALUE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_pd_counter_value)
- [NDIS_PD_FILTER_COUNTER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_pd_filter_counter)
- [NDIS_PD_FILTER_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_pd_filter_parameters)
- [NDIS_PD_ON_RSS_QUEUE_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)
- [NDIS_PD_OPEN_PROVIDER_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_pd_open_provider_parameters)
- [NDIS_PD_PROVIDER_DISPATCH](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_pd_provider_dispatch)
- [NDIS_PD_QUEUE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_pd_queue)
- [NDIS_PD_QUEUE_DISPATCH](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_pd_queue_dispatch)
- [NDIS_PD_QUEUE_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_pd_queue_parameters)
- [NDIS_PD_RECEIVE_QUEUE_COUNTER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_pd_receive_queue_counter)
- [NDIS_PD_TRANSMIT_QUEUE_COUNTER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_pd_transmit_queue_counter)
- [PD_BUFFER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_pd_buffer)
- [PD_BUFFER_8021Q_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_pd_buffer_8021q_info)
- [PD_BUFFER_VIRTUAL_SUBNET_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_pd_buffer_virtual_subnet_info)

### <a name="updated-data-structures"></a>更新后的数据结构

在 NDIS 6.50 中更新了以下数据结构。

- [NET_PNP_EVENT_NOTIFICATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_pnp_event_notification)
- [NDIS_OID_REQUEST](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)
- [NDIS_NET_BUFFER_LIST_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ne-ndis-_ndis_net_buffer_list_info)
- [NdisMGetDeviceProperty](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismgetdeviceproperty)
- [NDIS_SWITCH_OPTIONAL_HANDLERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_optional_handlers)
- [NDIS_SWITCH_NIC_SAVE_STATE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)

## <a name="ndis-651"></a>NDIS 6.51

NDIS 6.51 是非常次要版本更新到 NDIS 6.50。 NDIS 6.51 包含在 Windows 10，版本 1511年及更高版本。 NDIS 6.50 的所有信息也都适用于 NDIS 6.51 有以下例外：

- MinorNdisVersion 更改从 50 到 51 个向 NDIS 注册您的驱动程序时。
- 编译器设置更改从```NDIS650_MINIPORT=1```微型端口驱动程序和```NDIS650=1```筛选器或协议驱动程序，请向```NDIS651_MINIPORT=1```和```NDIS651=1```分别。

