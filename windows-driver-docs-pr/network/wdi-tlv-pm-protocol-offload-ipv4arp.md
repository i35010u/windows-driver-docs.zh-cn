---
title: WDI_TLV_PM_PROTOCOL_OFFLOAD_IPv4ARP
description: WDI_TLV_PM_PROTOCOL_OFFLOAD_IPv4ARP 是包含 IPv4 ARP 协议 TLV 卸载参数。
ms.assetid: 03894B22-3D4B-4262-893A-660FC88AA93D
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_PM_PROTOCOL_OFFLOAD_IPv4ARP 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 8b426057bb389c3c544af1f2417c176c9ce9c009
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373858"
---
# <a name="wditlvpmprotocoloffloadipv4arp"></a>WDI\_TLV\_PM\_PROTOCOL\_OFFLOAD\_IPv4ARP


WDI\_TLV\_PM\_协议\_卸载\_IPv4ARP 是 TLV 包含 IPv4 ARP 协议卸载参数。

## <a name="tlv-type"></a>TLV 类型


0x61

## <a name="length"></a>长度


所有包含的元素的大小的总和 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                              | 描述                                                                                                                                                                                                                                                                                                                                                                   |
|---------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT32                                            | 指定协议卸载 id。 这是一个操作系统提供的值，标识已卸载的协议。 操作系统向下发送添加请求或对基础驱动程序的请求完成之前，为在协议中唯一值的 OS 集 ProtocolOffloadId 将卸载网络适配器上。                                                                   |
| UINT8\[4\]                                        | 指定要与 ARP 请求的源协议地址 (SPA) 字段匹配的可选 IPv4 地址。 如果传入的 ARP 请求包含与此 IPv4 地址相匹配的 SPA 值，网络适配器会发送 ARP 响应处于低功耗状态时。 如果设置为零，网络适配器应响应 ARP 请求来自任何远程的 IPv4 地址。 |
| UINT8\[4\]                                        | 指定为源协议地址 (SPA) 字段中发送 ARP 响应时的网络适配器使用的主机 IPv4 地址。                                                                                                                                                                                                                                            |
| [**WDI\_MAC\_ADDRESS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_wdi_mac_address) | 指定的网络适配器必须使用它生成 ARP 响应数据包的源硬件地址 (SHA) 字段的 MAC 地址。 但是，它应为 MAC 标头中的源地址使用的网络适配器的当前 MAC 地址。                                                                                                          |

 

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
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




