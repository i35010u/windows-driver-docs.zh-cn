---
title: NDIS 6.50 简介
description: 本部分介绍了 NDIS 6.50，并介绍了 NDIS 6.40 中的更改。 NDIS 6.50 包含在 Windows 10 版本1507及更高版本中。
ms.assetid: 8D2EA09D-3FA3-467B-861A-AA15C790FCD3
ms.date: 06/01/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0370193a95eb2d9ef19da8005114e50f09999779
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844170"
---
# <a name="introduction-to-ndis-650"></a>NDIS 6.50 简介

本主题介绍网络驱动程序接口规范（NDIS）6.50，并介绍其主要的设计添加内容。 NDIS 6.50 包含在 Windows 10 版本1507及更高版本中。

NDIS 6.50 是 NDIS 6.40 的次要版本更新。 有关将 NDIS 1.x 驱动程序移植到 NDIS 6.50 的详细信息，请参阅[将 ndis 1.x 驱动程序移植到 ndis 6.50](porting-ndis-6-x-drivers-to-ndis-6-50.md)。

## <a name="feature-updates"></a>功能更新

NDIS 6.50 是 NDIS 6.40 的增量更新，不包含任何主要的新功能。

## <a name="implementing-an-ndis-650-driver"></a>实现 NDIS 6.50 驱动程序

NDIS 6.50 驱动程序必须遵循在[实现 NDIS 6.30 驱动程序](implementing-an-ndis-6-30-driver.md)中定义的要求。

此外，NDIS 6.50 驱动程序必须符合以下要求：

- 当 ndis 6.50 驱动程序使用 NDIS 注册时，它必须报告正确的 NDIS 版本。
   
   必须更新 NDIS_Xxx_DRIVER_CHARACTERISTICS 结构中的主要和次要 NDIS 版本号，才能支持 NDIS 6.50。 MajorNdisVersion 成员必须包含6个，并且 MinorNdisVersion 成员必须包含50。 此要求适用于微型端口、协议和筛选器驱动程序。 还必须更新编译器的版本信息（请参阅[编译 NDIS 6.50 驱动程序](#compiling-an-ndis-650-driver)）。

- 适用于 Windows 10 版本1507及更高版本的 NDIS 6.50 微型端口驱动程序必须使用 NDIS 6.50 版本的数据结构。 有关详细信息，请参阅[使用 NDIS 6.50 数据结构](#using-ndis-650-data-structures)。

## <a name="compiling-an-ndis-650-driver"></a>编译 NDIS 6.50 驱动程序

适用于 Windows 10 版本1507的 WDK 支持标头版本控制。 标头版本控制可确保 NDIS 6.50 驱动程序在编译时使用合适的 NDIS 6.50 数据结构。

将以下编译器设置添加到你的驱动程序的 Visual Studio 项目中：

- 对于微型端口驱动程序，请添加 ```NDIS650_MINIPORT=1```。
- 对于筛选器或协议驱动程序，请添加 ```NDIS650=1```。

有关使用 Windows 10 1507 版的 WDK 构建驱动程序的信息，请参阅[构建驱动程序](../develop/building-a-driver.md)。

## <a name="using-ndis-650-data-structures"></a>使用 NDIS 6.50 数据结构

### <a name="new-data-structures"></a>新数据结构

以下数据结构是在 NDIS 6.50 中新增的。

- [OID_WWAN_SYS_CAPS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-sys-caps)
- [OID_WWAN_DEVICE_CAPS_EX](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-device-caps-ex)
- [OID_WWAN_SLOT_INFO_STATUS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-slot-info-status)
- [OID_WWAN_NETWORK_IDLE_HINT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-network-idle-hint) 
- [NDIS_STATUS_PD_CURRENT_CONFIG](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pd-current-config)
- [NDIS_PD_CAPABILITIES](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pd_capabilities)
- [NDIS_PD_CLOSE_PROVIDER_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_pd_close_provider_parameters)
- [NDIS_PD_CONFIG](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pd_config)
- [NDIS_PD_COUNTER_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_pd_counter_parameters)
- [NDIS_PD_COUNTER_VALUE](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_pd_counter_value)
- [NDIS_PD_FILTER_COUNTER](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_pd_filter_counter)
- [NDIS_PD_FILTER_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_pd_filter_parameters)
- [NDIS_PD_ON_RSS_QUEUE_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)
- [NDIS_PD_OPEN_PROVIDER_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_pd_open_provider_parameters)
- [NDIS_PD_PROVIDER_DISPATCH](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_pd_provider_dispatch)
- [NDIS_PD_QUEUE](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_pd_queue)
- [NDIS_PD_QUEUE_DISPATCH](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_pd_queue_dispatch)
- [NDIS_PD_QUEUE_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_pd_queue_parameters)
- [NDIS_PD_RECEIVE_QUEUE_COUNTER](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_pd_receive_queue_counter)
- [NDIS_PD_TRANSMIT_QUEUE_COUNTER](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_pd_transmit_queue_counter)
- [PD_BUFFER](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_pd_buffer)
- [PD_BUFFER_8021Q_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_pd_buffer_8021q_info)
- [PD_BUFFER_VIRTUAL_SUBNET_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_pd_buffer_virtual_subnet_info)

### <a name="updated-data-structures"></a>更新的数据结构

以下数据结构已在 NDIS 6.50 中更新。

- [NET_PNP_EVENT_NOTIFICATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_pnp_event_notification)
- [NDIS_OID_REQUEST](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)
- [NDIS_NET_BUFFER_LIST_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ne-ndis-_ndis_net_buffer_list_info)
- [NdisMGetDeviceProperty](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismgetdeviceproperty)
- [NDIS_SWITCH_OPTIONAL_HANDLERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_optional_handlers)
- [NDIS_SWITCH_NIC_SAVE_STATE](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)

## <a name="ndis-651"></a>NDIS 6.51

对于 NDIS 6.50，NDIS 6.51 是一种非常小的版本更新。 NDIS 6.51 包含在 Windows 10 版本1511及更高版本中。 NDIS 6.50 的所有信息也适用于 NDIS 6.51，但有以下例外：

- 向 NDIS 注册驱动程序时，MinorNdisVersion 将从50更改为51。
- 对于微端口驱动程序，编译器设置和筛选器或协议驱动程序的 ```NDIS650=1``` ```NDIS650_MINIPORT=1``` 会分别更改为 ```NDIS651_MINIPORT=1``` 和 ```NDIS651=1```。

