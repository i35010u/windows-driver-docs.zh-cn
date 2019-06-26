---
title: OID_WDI_SET_P2P_LISTEN_STATE
description: OID_WDI_SET_P2P_LISTEN_STATE 端口上设置的 Wi-Fi Direct 的侦听状态。
ms.assetid: d488903b-ef64-44b6-b07a-70168a0ccfd8
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_SET_P2P_LISTEN_STATE 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 0f4d5ad2beb345db52457b05071a71c61ef1304f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359193"
---
# <a name="oidwdisetp2plistenstate"></a>OID\_WDI\_SET\_P2P\_LISTEN\_STATE


OID\_WDI\_设置\_P2P\_侦听\_状态的端口上设置的 Wi-Fi Direct 侦听状态。

| 范围 | 设置与任务序列化 | 正常执行时间 （秒） |
|-------|--------------------------|---------------------------------|
| Port  | 是                      | 1                               |

 

有不同级别的侦听状态，端口需遵守在端口之间的并发要求。

此属性才适用于虚拟化 Wi-Fi Direct 适配器端口接口。

当侦听状态处于活动状态时，端口应一段时间的社交通道上放置单选。

如果该适配器具有非社交通道上运行的虚拟化的端口，端口可能会发现该通道上。 如果使用此行为，则该端口必须是非常高度可用，以允许其他适配器，以快速发现它在 Wi-Fi Direct 发现扫描阶段时。 这可提供作为以避免在低延迟方案跳跃通道的权衡。

**请注意**  此属性指定单选时间切片要求将与其他属性或颁发给该端口的任务可能会导致冲突的端口。

 

## <a name="set-property-parameters"></a>设置属性参数


| TLV                                                                         | 允许多个 TLV 实例 | 可选 | 描述                                                                                                                                                      |
|-----------------------------------------------------------------------------|--------------------------------|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_P2P\_LISTEN\_STATE**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-listen-state)       |                                |          | 所需的侦听状态。                                                                                                                                            |
| [**WDI\_TLV\_P2P\_CHANNEL\_NUMBER**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-channel-number)   |                                | X        | 主机的所需的侦听通道时启用 Wi-Fi Direct 侦听状态。 如果未指定此选项，端口可能会选择在其自己的侦听通道。 |
| [**WDI\_TLV\_P2P\_侦听\_持续时间**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-listen-duration) |                                |          | 周期持续时间和侦听时间。                                                                                                                                  |

 

## <a name="set-property-results"></a>设置属性结果


没有其他数据。 标头中的数据就足够了。

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

 

 




