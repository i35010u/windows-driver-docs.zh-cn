---
title: OID_WDI_SET_P2P_START_BACKGROUND_DISCOVERY
description: OID_WDI_SET_P2P_START_BACKGROUND_DISCOVERY 指示适配器在后台定期执行 Wi-fi 直接发现
ms.assetid: DF58B71D-7D45-4E0D-963F-A70471363DF5
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_SET_P2P_START_BACKGROUND_DISCOVERY 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 58601a60e1fd095d7ba6f7aa1bf437957aa1064f
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215821"
---
# <a name="oid_wdi_set_p2p_start_background_discovery"></a>OID \_ WDI \_ 设置 \_ P2P \_ 开始 \_ 后台 \_ 发现


OID \_ WDI \_ 设置 \_ P2P \_ 开始 \_ 后台 \_ 发现指示适配器在后台定期执行 wi-fi 直接发现

| 作用域 | 设置序列化任务 | 正常执行时间 (秒)  | 影响数据吞吐量/延迟 |
|-------|--------------------------|---------------------------------|---------------------------------|
| 端口  | 否                       | 1                               | 是                             |

 

适配器需要按固定的时间间隔扫描指定的通道，并且能够查找设备可见性超时内可发现的设备， (通常为5分钟) 。 此行为类似于 [OID \_ WDI \_ 任务 \_ P2P \_ 探索](oid-wdi-task-p2p-discover.md)) 中定义的常规 wi-fi 直接发现扫描 (，但它不是时间限制的，并且适配器可能会在以后的某个时间点计划扫描。 适配器必须在每个设备的可见性超时内执行至少一次扫描。 如果设备可见性超时值为0，则适配器应继续使用其自己的周期时间定期扫描。 如果在这段时间内发出了发现或扫描任务请求，则适配器应在任务持续期间挂起后台发现，并在任务完成时继续执行。 完成后台扫描后，设备应发送 [NDIS \_ 状态 \_ WDI \_ 指示 \_ P2P \_ DISCOVERY \_ 完成](ndis-status-wdi-indication-p2p-discovery-complete.md) 指示 (并且事务 ID 等于 0) ，以使操作系统知道它已完成扫描。 每次完成后台扫描时，适配器都必须发送此指示。

如果提供了通道列表，则适配器只应扫描指定的通道。 否则，它应扫描所有通道。 如果固件在指定的通道之外发现设备，则仍应将信息发送到操作系统。

如果指定了侦听持续时间和通道 ([**WDI \_ TLV \_ \_ 发现 \_ 通道 \_ 设置**](./wdi-tlv-p2p-discovery-channel-settings.md)) ，则它们表示远程设备的侦听时间。 根据侦听持续时间和通道的所有值，适配器需要以最有效的方式来扫描请求的通道。 操作系统还可以指定多个侦听持续时间和通道实例。 在这种情况下，适配器应该首先为具有非零值 "侦听时间" 和 "频道列表" 的条目提供扫描计划。 然后，在以下情况下，适配器应使用默认值：

1.  如果侦听持续时间为0，则适配器应为指定的通道使用默认扫描时间。
2.  如果 "通道列表" 为空，则适配器应使用为该带区指定的侦听和循环时间扫描这些通道中的所有通道。 扫描时间不适用于具有操作系统指定的单独侦听持续时间的任何通道。

如果 NIC 为 D0，适配器将指示对特定服务名称的探测请求的响应 () 为 [NDIS \_ 状态 \_ WDI \_ 指示 \_ BSS \_ \_ 列表](ndis-status-wdi-indication-bss-entry-list.md) 通知到操作系统。 WDI 缓存更高层服务的操作系统的响应信息，并根据需要进行通知。

当 NIC 在 D2 中时，它会挂起后台发现，直到它恢复到 D0 状态。

## <a name="set-property-parameters"></a>设置属性参数


| TLV                                                                                                | 允许多个 TLV 实例 | 可选 | 说明                                                                                                                         |
|----------------------------------------------------------------------------------------------------|--------------------------------|----------|-------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI \_ TLV \_ P2P \_ 后台 \_ 发现 \_ 模式**](./wdi-tlv-p2p-background-discover-mode.md)     |                                |          | Wi-fi Direct 后台发现模式参数。                                                                                   |
| [**WDI \_ TLV \_ P2P \_ 发现 \_ 通道 \_ 设置**](./wdi-tlv-p2p-discovery-channel-settings.md) | X                              | X        | 要扫描的建议通道的列表。                                                                                               |
| [**WDI \_ TLV \_ P2P \_ 设备 \_ 筛选器 \_ 列表**](./wdi-tlv-p2p-device-filter-list.md)                 |                                | X        | 在 Wi-fi Direct 设备发现期间要搜索的 Wi-fi Direct 设备和组所有者列表。                                    |
| [**WDI \_ TLV \_ P2P \_ 服务 \_ 名称 \_ 哈希**](./wdi-tlv-p2p-service-name-hash.md)                   | X                              | X        | 要查询的服务哈希名称的列表。 如果 \_ \_ \_ \_ \_ \_ \_ 仅指定了 WDI P2P 服务发现类型服务名称，则这是必需的。 |
| [**WDI \_ TLV \_ 供应商 \_ 特定 \_ IE**](./wdi-tlv-vendor-specific-ie.md)                          |                                | X        | 必须包含在端口发送的探测请求中的一个或多个传入。                                                       |

 

## <a name="set-property-results"></a>设置属性结果


无其他数据。 标头中的数据足够了。
## <a name="unsolicited-indication"></a>未经请求的指示


[NDIS \_ 状态 \_ WDI \_ 指示 \_ BSS \_ 条目 \_ 列表](ndis-status-wdi-indication-bss-entry-list.md)

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>最低受支持的客户端</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>最低受支持的服务器</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Dot11wdi</td>
</tr>
</tbody>
</table>

 

