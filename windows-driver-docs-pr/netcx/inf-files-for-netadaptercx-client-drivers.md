---
title: NetAdapterCx 客户端驱动程序的 INF 文件
description: NetAdapterCx 客户端驱动程序的 INF 文件
ms.assetid: B885CDF7-B399-440B-A385-27F1090B9C56
keywords:
- NetAdapterCx 客户端驱动程序，NetCx INF 文件 NetAdapterCx INF 的 INF 文件
ms.date: 08/13/2018
ms.localizationpriority: medium
ms.openlocfilehash: 5265147b4d1bd47c16f0e46ba5dc4508d805fd4f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384548"
---
# <a name="inf-files-for-netadaptercx-client-drivers"></a>NetAdapterCx 客户端驱动程序的 INF 文件

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

NetAdapterCx 客户端驱动程序的 INF 文件生成基于标准网络 INF 文件，使用特定于 NetAdapterCx 某些其他关键字。 

有关标准网络 INF 文件的详细信息，请参阅[创建网络 INF 文件](../network/creating-network-inf-files.md)。 有关基本 INF 文件的详细信息，请参阅[INF 文件的部分和指令](../install/inf-file-sections-and-directives.md)。

下表介绍 NetAdapterCx 中新的 INF 关键字。

| 新的网络关键字 | INF 文件部分 | 可选或必需 | 描述 |
| --- | --- | --- | --- |
| **\*IfConnectorPresent** | Device.NT | 必需 | <p>一个布尔值，该值指示连接器是否存在。 将此关键字设置为**1**，或**TRUE**，如果没有物理适配器。</p> <p>**请注意**取代**IfConnectorPresent**字段从[ **NDIS_MINIPORT_ADAPTER_GENERAL_ATTRIBUTES** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)结构。</p> |
| **\*ConnectionType** | Device.NT | 必需 | 一个[ **NET_IF_CONNECTION_TYPE** ](https://docs.microsoft.com/windows/desktop/api/ifdef/ne-ifdef-_net_if_connection_type)值，该值指定[NDIS 网络接口](../network/ndis-network-interfaces2.md)连接类型。 |
| **\*DirectionType** | Device.NT | 必需 | 一个[ **NET_IF_DIRECTION_TYPE** ](https://docs.microsoft.com/windows/desktop/api/ifdef/ne-ifdef-_net_if_direction_type)值，该值指定[NDIS 网络接口](../network/ndis-network-interfaces2.md)方向类型。 |
| **\*AccessType** | Device.NT | 必需 | 一个[ **NET_IF_ACCESS_TYPE** ](https://docs.microsoft.com/windows/desktop/api/ifdef/ne-ifdef-_net_if_access_type)值，该值指定[NDIS 网络接口](../network/ndis-network-interfaces2.md)访问类型。 |
| **\*HardwareLoopback** | Device.NT | 必需 | <p>一个布尔值，该值指示是否网络接口卡 (NIC) 具有硬件环回支持。</p> <p>**请注意**将此关键字设置为**1**，或**TRUE**，相当于**不**设置**NDIS_MAC_OPTION_NO_LOOPBACK**中的标志**MacOptions**字段[ **NDIS_MINIPORT_ADAPTER_GENERAL_ATTRIBUTES** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)结构。</p> |
| **NumberOfNetworkInterfaces** | Device.NT | 可选 | 指定的网络接口数量 NIC 支持。 才被必需的 NIC 是否支持每个设备的多个网络接口。 |

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
