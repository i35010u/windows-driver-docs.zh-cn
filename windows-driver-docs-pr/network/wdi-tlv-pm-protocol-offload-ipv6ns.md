---
title: WDI_TLV_PM_PROTOCOL_OFFLOAD_IPv6NS
description: WDI_TLV_PM_PROTOCOL_OFFLOAD_IPv6NS 是包含 IPv6 NS 协议卸载参数的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_PM_PROTOCOL_OFFLOAD_IPv6NS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: d92cdd9d0dc9d46a0b05de56bf26cd5b2f144361
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834283"
---
# <a name="wdi_tlv_pm_protocol_offload_ipv6ns"></a>WDI \_ TLV \_ PM \_ 协议 \_ 卸载 \_ IPv6NS


WDI \_ tlv \_ PM \_ 协议 \_ 卸载 \_ IPv6NS 是包含 IPv6 NS 协议卸载参数的 tlv。

## <a name="tlv-type"></a>TLV 类型


0x62

## <a name="length"></a>长度


Sum (所有包含的元素的大小) 。

## <a name="values"></a>值


| 类型                                              | 描述                                                                                                                                                                                                                                                                                                                                                                                                    |
|---------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT32                                            | 指定协议卸载 ID。 这是操作系统提供的用于标识卸载协议的值。 在 OS 向下发送添加请求或完成对过量驱动程序的请求之前，操作系统会将 ProtocolOffloadId 设置为在网络适配器上的协议卸载之间唯一的值。                                                                                                    |
| UINT8 \[ 16\]                                       | 指定要与 NS 消息的 IPv6 标头中的 "源地址" 字段匹配的可选 IPv6 地址。 如果传入的 NS 消息具有与此 IPv6 地址相匹配的源地址值，网络适配器将在处于低功耗状态 (NA) 消息时发送邻居播发。 如果此值设置为零，则网络适配器应响应来自任何远程 IPv6 地址的 NS 消息。 |
| UINT8 \[ 16\]                                       | 指定请求的节点 IPv6 地址。                                                                                                                                                                                                                                                                                                                                                                     |
| UINT8 \[ 16\]                                       | 指定一个或两个 IPv6 地址以匹配传入 NS 消息的目标地址字段。 如果只有一个地址，则该地址存储在目标地址1中，目标地址2用零填充。 如果其中一个地址与传入 NS 消息的 "目标地址" 字段相匹配，则该网络适配器会在响应中发送一条 NA 消息。                                               |
| UINT8 \[ 16\]                                       | 请参阅目标地址1的说明。                                                                                                                                                                                                                                                                                                                                                                           |
| [**WDI \_ MAC \_ 地址**](/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address) | 指定网络适配器必须用于其生成的 NA 消息 (TLLA) "字段的目标链路层地址的 MAC 地址。 但是，它应该使用网络适配器的当前 MAC 地址作为 MAC 标头中的源地址。                                                                                                                                                 |

 

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
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

