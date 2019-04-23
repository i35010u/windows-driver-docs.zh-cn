---
title: OID_WDI_SET_P2P_START_BACKGROUND_DISCOVERY
description: OID_WDI_SET_P2P_START_BACKGROUND_DISCOVERY 指示要在后台定期执行 Wi-Fi Direct 发现的适配器
ms.assetid: DF58B71D-7D45-4E0D-963F-A70471363DF5
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_SET_P2P_START_BACKGROUND_DISCOVERY 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: d6f0549dbe26b7cf65eaa2ae7447f306c858a194
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59902375"
---
# <a name="oidwdisetp2pstartbackgrounddiscovery"></a>OID\_WDI\_设置\_P2P\_启动\_背景\_发现


OID\_WDI\_设置\_P2P\_启动\_背景\_发现指示要在后台定期执行 Wi-Fi Direct 发现的适配器

| 范围 | 设置与任务序列化 | 正常执行时间 （秒） | 影响数据吞吐量/延迟 |
|-------|--------------------------|---------------------------------|---------------------------------|
| 端口  | 否                       | 1                               | 是                             |

 

适配器需要扫描按固定间隔的指定的通道，并在找到可以被检测到设备的可见性超时 （通常为 5 分钟） 内的设备。 行为是类似于常规的 Wi-Fi Direct 发现扫描 (中定义[OID\_WDI\_任务\_P2P\_发现](oid-wdi-task-p2p-discover.md))，但它不是时间密集型和适配器可能计划在某个时间点更高版本扫描。 适配器必须执行每个设备的可见性超时内至少一次扫描。 如果设备的可见性超时值为 0，适配器应继续扫描定期使用其自己的周期时间。 如果发现或扫描任务请求时，在此期间，适配器应挂起任务的持续时间内的后台发现，然后继续任务完成。 设备应在完成后台扫描，请发送[NDIS\_状态\_WDI\_指示\_P2P\_发现\_完成](ndis-status-wdi-indication-p2p-discovery-complete.md)（具有事务 ID 等于 0) 指示若要使操作系统知道它已完成一次扫描。 每次完成后台扫描时，适配器必须发送此指示。

如果提供的通道列表，则适配器应仅扫描对指定的通道。 否则，它应扫描的所有通道。 如果固件中发生来发现设备指定通道之外，它应仍发送到操作系统的信息。

当侦听持续时间和通道 ([**WDI\_TLV\_P2P\_发现\_通道\_设置**](https://msdn.microsoft.com/library/windows/hardware/dn897877)) 指定，则它们将引用到远程设备的侦听时间。 根据侦听持续时间和通道的所有值，适配器需要拿出一个计划以最高效的方式扫描请求的通道。 操作系统也可指定侦听持续时间和通道的多个实例。 在这种情况下，适配器应首先提出了这些条目将侦听的持续时间和通道列表的值为非零的扫描计划。 然后，适配器应在以下情况下使用默认值：

1.  如果侦听持续时间为 0，则适配器应指定通道使用默认的扫描时间。
2.  如果通道列表为空，适配器应扫描中的所有使用该带区的指定的侦听和周期时间带内通道。 扫描时间不会应用到任何具有单独的通道侦听由操作系统指定的持续时间。

适配器 D0 NIC 时，指示对特定服务的名称的探测请求的响应[NDIS\_状态\_WDI\_指示\_BSS\_条目\_列表](ndis-status-wdi-indication-bss-entry-list.md)通知到操作系统。 WDI 缓存对于更高的层服务，OS 的响应信息，并会根据需要通知他们。

D2 NIC 时，它将挂起后台发现，直到它回到 D0。

## <a name="set-property-parameters"></a>设置属性参数


| TLV                                                                                                | 允许多个 TLV 实例 | 可选 | 描述                                                                                                                         |
|----------------------------------------------------------------------------------------------------|--------------------------------|----------|-------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_P2P\_背景\_DISCOVER\_模式**](https://msdn.microsoft.com/library/windows/hardware/dn897864)     |                                |          | Wi-Fi Direct 背景发现模式的参数。                                                                                   |
| [**WDI\_TLV\_P2P\_发现\_通道\_设置**](https://msdn.microsoft.com/library/windows/hardware/dn897877) | X                              | X        | 建议的列表可扫描的通道。                                                                                               |
| [**WDI\_TLV\_P2P\_DEVICE\_FILTER\_LIST**](https://msdn.microsoft.com/library/windows/hardware/dn897873)                 |                                | X        | 发现 Wi-Fi Direct 设备和组所有者能够在 Wi-Fi Direct 设备期间搜索的列表。                                    |
| [**WDI\_TLV\_P2P\_SERVICE\_NAME\_HASH**](https://msdn.microsoft.com/library/windows/hardware/dn898009)                   | X                              | X        | 要查询的服务哈希名称的列表。 如果这是必需 WDI\_P2P\_服务\_发现\_类型\_服务\_名称\_只指定了。 |
| [**WDI\_TLV\_VENDOR\_SPECIFIC\_IE**](https://msdn.microsoft.com/library/windows/hardware/dn898076)                          |                                | X        | 必须包括在由端口发送的探测请求的一个或多个 Ie。                                                       |

 

## <a name="set-property-results"></a>设置属性结果


没有其他数据。 标头中的数据就足够了。
## <a name="unsolicited-indication"></a>未经请求的指示


[NDIS\_状态\_WDI\_指示\_BSS\_条目\_列表](ndis-status-wdi-indication-bss-entry-list.md)

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
<td><p>Header</p></td>
<td>Dot11wdi.h</td>
</tr>
</tbody>
</table>

 

 




