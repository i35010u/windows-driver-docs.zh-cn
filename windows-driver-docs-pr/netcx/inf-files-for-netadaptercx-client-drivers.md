---
title: NetAdapterCx 客户端驱动程序的 INF 文件
description: NetAdapterCx 客户端驱动程序的 INF 文件
ms.assetid: B885CDF7-B399-440B-A385-27F1090B9C56
keywords:
- 用于 NetAdapterCx 客户端驱动程序的 INF 文件、NetCx INF 文件、NetAdapterCx INF
ms.date: 08/13/2018
ms.localizationpriority: medium
ms.openlocfilehash: 3f8638c46f73a09eed74f3bc0d02bdc72952a20d
ms.sourcegitcommit: 20a89aa2cb2c6385c2a49ebf78e5797c821d87ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/31/2020
ms.locfileid: "87473733"
---
# <a name="inf-files-for-netadaptercx-client-drivers"></a>NetAdapterCx 客户端驱动程序的 INF 文件

用于 NetAdapterCx 客户端驱动程序的 INF 文件在标准网络 INF 文件的基础上构建，并且有一些特定于 NetAdapterCx 的其他关键字。 

有关标准网络 INF 文件的详细信息，请参阅[创建网络 Inf 文件](../network/creating-network-inf-files.md)。 有关基本 INF 文件的详细信息，请参阅[INF 文件概述](../install/overview-of-inf-files.md)。

下表介绍了 NetAdapterCx 中的新 INF 关键字。

| 新建网络关键字 | INF 文件部分 | 可选或必需 | 描述 |
| --- | --- | --- | --- |
| **\*IfConnectorPresent** | Device NT | 必须 | <p>指示连接器是否存在的布尔值。 如果有物理适配器，则将此关键字设置为**1**或**TRUE**。</p> <p>**注意**替换[**NDIS_MINIPORT_ADAPTER_GENERAL_ATTRIBUTES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)结构中的**IfConnectorPresent**字段。</p> |
| **\*ConnectionType** | Device NT | 必须 | 一个[**NET_IF_CONNECTION_TYPE**](https://docs.microsoft.com/windows/desktop/api/ifdef/ne-ifdef-_net_if_connection_type)值，该值指定[NDIS 网络接口](../network/ndis-network-interfaces2.md)连接类型。 |
| **\*DirectionType** | Device NT | 必须 | 一个[**NET_IF_DIRECTION_TYPE**](https://docs.microsoft.com/windows/desktop/api/ifdef/ne-ifdef-_net_if_direction_type)值，该值指定[NDIS 网络接口](../network/ndis-network-interfaces2.md)方向类型。 |
| **\*AccessType** | Device NT | 必须 | 一个[**NET_IF_ACCESS_TYPE**](https://docs.microsoft.com/windows/desktop/api/ifdef/ne-ifdef-_net_if_access_type)值，该值指定[NDIS 网络接口](../network/ndis-network-interfaces2.md)访问类型。 |
| **\*HardwareLoopback** | Device NT | 必须 | <p>一个布尔值，该值指示网络接口卡（NIC）是否有硬件环回支持。</p> <p>**注意**将此关键字设置为**1**或**TRUE**等效于**不**设置[**NDIS_MINIPORT_ADAPTER_GENERAL_ATTRIBUTES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)结构的**MacOptions**字段中的**NDIS_MAC_OPTION_NO_LOOPBACK**标志。</p> |
| **NumberOfNetworkInterfaces** | Device NT | 可选 | 指定 NIC 支持的网络接口数。 仅当 NIC 支持每个设备有多个网络接口时，才需要。 |

例如：

```INF
[Device.NT]
CopyFiles=Drivers_Dir

; Existing network keywords
*IfType       = 6
*MediaType     = 0
*PhysicalMediaType = 14

; New network keywords
*IfConnectorPresent = 1     ; BOOLEAN
*ConnectionType   = 1       ; NET_IF_CONNECTION_TYPE
*DirectionType   = 0        ; NET_IF_DIRECTION_TYPE
*AccessType     = 2         ; NET_IF_ACCESS_TYPE
*HardwareLoopback  = 0      ; BOOLEAN
NumberOfNetworkInterfaces = 11
```
