---
title: OID_WDI_SET_P2P_LISTEN_STATE
description: OID_WDI_SET_P2P_LISTEN_STATE 设置端口上的 Wi-Fi 直接侦听状态。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_SET_P2P_LISTEN_STATE 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: fa6485c21e6a8224731777b8facda1d84c84d8b7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829351"
---
# <a name="oid_wdi_set_p2p_listen_state"></a>OID \_ WDI \_ 设置 \_ P2P \_ 侦听 \_ 状态


OID \_ WDI \_ SET \_ P2P \_ 侦听 \_ 状态设置端口上 Wi-Fi 直接侦听状态。

| 范围 | 设置序列化任务 | 正常执行时间 (秒)  |
|-------|--------------------------|---------------------------------|
| 端口  | 是                      | 1                               |

 

有不同级别的侦听状态，并且端口应符合端口间的并发要求。

此属性仅适用于虚拟化的 Wi-Fi 直接适配器端口接口。

当 "侦听" 状态处于活动状态时，该端口应在某个时间段内将收音机置于社交通道上。

如果适配器具有在非社交通道上操作的虚拟化端口，则该端口可能会在该通道上变为可发现。 如果使用此行为，则端口必须高度可用，以允许其他适配器在 Wi-Fi 直接发现的扫描阶段中快速发现它。 这是为了避免在低延迟方案中跳过通道而进行的权衡。

**注意**  此属性指定对端口的无线电时间片要求，这可能会导致与颁发给该端口的其他属性或任务冲突。

 

## <a name="set-property-parameters"></a>设置属性参数


| TLV                                                                         | 允许多个 TLV 实例 | 可选 | 说明                                                                                                                                                      |
|-----------------------------------------------------------------------------|--------------------------------|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI \_ TLV \_ P2P \_ 侦听 \_ 状态**](./wdi-tlv-p2p-listen-state.md)       |                                |          | 所需的侦听状态。                                                                                                                                            |
| [**WDI \_ TLV \_ P2P \_ 信道 \_ 号**](./wdi-tlv-p2p-channel-number.md)   |                                | X        | 启用 Wi-Fi 直接侦听状态时，主机所需的侦听通道。 如果未指定此选项，则端口可以自行选择侦听通道。 |
| [**WDI \_ TLV \_ P2P \_ 侦听 \_ 持续时间**](./wdi-tlv-p2p-listen-duration.md) |                                |          | 周期持续时间和侦听时间。                                                                                                                                  |

 

## <a name="set-property-results"></a>设置属性结果


无其他数据。 标头中的数据足够了。

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
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Dot11wdi</td>
</tr>
</tbody>
</table>

 

