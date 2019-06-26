---
title: WDI_TLV_PM_PROTOCOL_OFFLOAD_IPv6NS
description: WDI_TLV_PM_PROTOCOL_OFFLOAD_IPv6NS 是包含 IPv6 NS 协议 TLV 卸载参数。
ms.assetid: 0385449B-82C6-44B4-BBD3-A708ADE54AC4
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_PM_PROTOCOL_OFFLOAD_IPv6NS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 40be32b1e51fab0c877cdb1fe99c130691be4c8f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373851"
---
# <a name="wditlvpmprotocoloffloadipv6ns"></a>WDI\_TLV\_PM\_PROTOCOL\_OFFLOAD\_IPv6NS


WDI\_TLV\_PM\_协议\_卸载\_IPv6NS 是 TLV 包含 IPv6 NS 协议卸载参数。

## <a name="tlv-type"></a>TLV 类型


0x62

## <a name="length"></a>长度


所有包含的元素的大小的总和 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                              | 描述                                                                                                                                                                                                                                                                                                                                                                                                    |
|---------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT32                                            | 指定协议卸载 id。 这是一个操作系统提供的值，标识已卸载的协议。 操作系统向下发送添加请求或对基础驱动程序的请求完成之前，为在协议中唯一值的 OS 集 ProtocolOffloadId 将卸载网络适配器上。                                                                                                    |
| UINT8\[16\]                                       | 指定要与 NS 消息的 IPv6 标头中的源地址字段匹配的可选 IPv6 地址。 如果传入的 NS 消息具有值的源地址匹配此 IPv6 地址，网络适配器发送的邻居播发 (NA) 消息时处于低功耗状态。 如果设置为零，则网络适配器应响应的 NS 消息来自任何远程的 IPv6 地址。 |
| UINT8\[16\]                                       | 指定经请求的节点的 IPv6 地址。                                                                                                                                                                                                                                                                                                                                                                     |
| UINT8\[16\]                                       | 指定一个或两个 IPv6 地址以匹配传入 NS 消息的目标地址字段。 如果只有一个地址，该地址存储在目标地址为 1，并且目标地址 2 填充了零。 如果传入 NS 消息的目标地址字段匹配其中一个地址，网络适配器在响应中发送 NA 消息。                                               |
| UINT8\[16\]                                       | 请参阅目标地址 1 的说明。                                                                                                                                                                                                                                                                                                                                                                           |
| [**WDI\_MAC\_ADDRESS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_wdi_mac_address) | 指定的网络适配器必须使用它生成的 NA 消息的目标链路层地址 (TLLA) 字段的 MAC 地址。 但是，它应为 MAC 标头中的源地址使用的网络适配器的当前 MAC 地址。                                                                                                                                                 |

 

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

 

 




