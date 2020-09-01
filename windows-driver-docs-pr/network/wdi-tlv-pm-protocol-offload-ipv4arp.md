---
title: WDI_TLV_PM_PROTOCOL_OFFLOAD_IPv4ARP
description: WDI_TLV_PM_PROTOCOL_OFFLOAD_IPv4ARP 是包含 IPv4 ARP 协议卸载参数的 TLV。
ms.assetid: 03894B22-3D4B-4262-893A-660FC88AA93D
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_PM_PROTOCOL_OFFLOAD_IPv4ARP 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 03dbad93cd4b8a32134cf9ed64d261eda737a926
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89209247"
---
# <a name="wdi_tlv_pm_protocol_offload_ipv4arp"></a>WDI \_ TLV \_ PM \_ 协议 \_ 卸载 \_ IPv4ARP


WDI \_ tlv \_ PM \_ 协议 \_ 卸载 \_ IPv4ARP 是包含 IPv4 ARP 协议卸载参数的 tlv。

## <a name="tlv-type"></a>TLV 类型


0x61

## <a name="length"></a>Length


Sum (所有包含的元素的大小) 。

## <a name="values"></a>值


| 类型                                              | 说明                                                                                                                                                                                                                                                                                                                                                                   |
|---------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT32                                            | 指定协议卸载 ID。 这是操作系统提供的用于标识卸载协议的值。 在 OS 向下发送添加请求或完成对过量驱动程序的请求之前，操作系统会将 ProtocolOffloadId 设置为在网络适配器上的协议卸载之间唯一的值。                                                                   |
| UINT8 \[ 4\]                                        | 指定要与 ARP 请求的 (SPA) 字段的源协议地址相匹配的可选 IPv4 地址。 如果传入 ARP 请求的 SPA 值与此 IPv4 地址相匹配，则当网络适配器处于低功耗状态时，它会发送 ARP 响应。 如果此值设置为零，则网络适配器应响应来自任何远程 IPv4 地址的 ARP 请求。 |
| UINT8 \[ 4\]                                        | 指定发送 ARP 响应时网络适配器用于源协议地址 (SPA) 字段的主机 IPv4 地址。                                                                                                                                                                                                                                            |
| [**WDI \_ MAC \_ 地址**](/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address) | 指定网络适配器必须用于其生成的 ARP 响应数据包 (SHA) 字段的源硬件地址的 MAC 地址。 但是，它应该使用网络适配器的当前 MAC 地址作为 MAC 标头中的源地址。                                                                                                          |

 

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
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

