---
title: WDI_TLV_CONNECT_BSS_ENTRY
description: WDI_TLV_CONNECT_BSS_ENTRY 是一个 TLV，其中包含候选连接 BSS 条目的列表。
ms.assetid: 0D74B2DE-9224-4FDF-8EA8-B22CEC0B5F26
ms.date: 07/18/2017
keywords:
- WDI_TLV_CONNECT_BSS_ENTRY 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 7ea2332b18377c8f467096d56ca28d98e32c93d7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843390"
---
# <a name="wdi_tlv_connect_bss_entry"></a>WDI\_TLV\_连接\_BSS\_条目


WDI\_TLV\_连接\_BSS\_条目是包含候选连接 BSS 条目列表的 TLV。

## <a name="tlv-type"></a>TLV 类型


0x34 赋

## <a name="length"></a>长度


所有包含的 TLVs 的大小的总和（以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                                                        | 允许多个 TLV 实例 | 可选 | 描述                                                                                                                                                   |
|---------------------------------------------------------------------------------------------|--------------------------------|----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_BSSID**](wdi-tlv-bssid.md)                                                    |                                |          | BSS 的 BSSID。                                                                                                                                         |
| [**WDI\_TLV\_探测\_响应\_帧**](wdi-tlv-probe-response-frame.md)                    |                                | X        | 探测响应帧。 如果未收到探测响应，则为空。                                                                        |
| [**WDI\_TLV\_信标\_帧**](wdi-tlv-beacon-frame.md)                                     |                                | X        | 信号框架。 如果未收到信号，则为空。                                                                                        |
| [**WDI\_TLV\_BSS\_条目\_信号\_信息**](wdi-tlv-bss-entry-signal-info.md)                 |                                |          | 此 BSS 条目的信号信息。                                                                                                                    |
| [**WDI\_TLV\_BSS\_条目\_通道\_信息**](wdi-tlv-bss-entry-channel-info.md)               |                                |          | 此 BSS 条目的通道信息。                                                                                                                   |
| [**WDI\_TLV\_BSS\_条目\_设备\_上下文**](wdi-tlv-bss-entry-device-context.md)           |                                | X        | IHV 提供有关此对等方的上下文数据。                                                                                                                |
| [**WDI\_TLV\_PMKID**](wdi-tlv-pmkid.md)                                                    |                                | X        | 此 BSS 条目的16字节 PMKID 值。                                                                                                                   |
| [**WDI\_TLV\_额外\_关联\_请求\_** ](wdi-tlv-extra-association-request-ies.md) |                                | X        | 要包含在此 BSSID 的（re）关联请求帧中的 IE。 如果存在，则除了常见的 IE 外，还应包括此项。                  |
| [**WDI\_TLV\_FT\_初始\_ASSOC\_参数**](wdi-tlv-ft-initial-assoc-parameters.md)     |                                | X        | 初始移动域关联参数。                                                                                                           |
| [**WDI\_TLV\_FT\_REASSOC\_参数**](wdi-tlv-ft-reassoc-parameters.md)                  |                                | X        | Fast 转换参数（MDIE、R0KH、PMKR0Name、SNonce）。 这仅用于快速转换（不是在初始移动域关联期间）。 |
| [**WDI\_TLV\_BSS\_选择\_参数**](wdi-tlv-bss-selection-parameters.md)            |                                | X        | [**WDI\_bss\_选择\_标志**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_bss_selection_flags)，这些标志提供主机用于 BSS 选择的信息。                               |

 

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
<td><p>Windows 10</p></td>
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

 

 




