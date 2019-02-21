---
title: WDI_TLV_CONNECT_BSS_ENTRY
description: WDI_TLV_CONNECT_BSS_ENTRY 是包含一组候选 TLV 连接 BSS 条目。
ms.assetid: 0D74B2DE-9224-4FDF-8EA8-B22CEC0B5F26
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_CONNECT_BSS_ENTRY 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: a1a86fe448f113dc8b59fffaddca2e586f0085da
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543538"
---
# <a name="wditlvconnectbssentry"></a>WDI\_TLV\_CONNECT\_BSS\_条目


WDI\_TLV\_CONNECT\_BSS\_项是包含一组候选 TLV 连接 BSS 条目。

## <a name="tlv-type"></a>TLV 类型


0x34

## <a name="length"></a>长度


所有的大小 （以字节为单位） 总和包含 TLVs。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                                                        | 允许多个 TLV 实例 | 可选 | 描述                                                                                                                                                   |
|---------------------------------------------------------------------------------------------|--------------------------------|----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_BSSID**](wdi-tlv-bssid.md)                                                    |                                |          | BSS BSSID。                                                                                                                                         |
| [**WDI\_TLV\_探测\_响应\_帧**](wdi-tlv-probe-response-frame.md)                    |                                | X        | 探测响应帧。 如果不收到任何探测响应，将为空。                                                                        |
| [**WDI\_TLV\_BEACON\_FRAME**](wdi-tlv-beacon-frame.md)                                     |                                | X        | 信号帧。 如果收到没有信号，将为空。                                                                                        |
| [**WDI\_TLV\_BSS\_条目\_信号\_信息**](wdi-tlv-bss-entry-signal-info.md)                 |                                |          | 此 BSS 项的信号信息。                                                                                                                    |
| [**WDI\_TLV\_BSS\_条目\_通道\_信息**](wdi-tlv-bss-entry-channel-info.md)               |                                |          | 此 BSS 项的通道信息。                                                                                                                   |
| [**WDI\_TLV\_BSS\_ENTRY\_DEVICE\_CONTEXT**](wdi-tlv-bss-entry-device-context.md)           |                                | X        | IHV 提供有关此对等方的上下文数据。                                                                                                                |
| [**WDI\_TLV\_PMKID**](wdi-tlv-pmkid.md)                                                    |                                | X        | 此 BSS 条目的 16 字节 PMKID 值。                                                                                                                   |
| [**WDI\_TLV\_EXTRA\_ASSOCIATION\_REQUEST\_IES**](wdi-tlv-extra-association-request-ies.md) |                                | X        | IE 要包含在 （重新） 中的此 BSSID 关联请求帧。 如果存在，这应包括除了常见的 IE。                  |
| [**WDI\_TLV\_FT\_初始\_ASSOC\_参数**](wdi-tlv-ft-initial-assoc-parameters.md)     |                                | X        | 初始移动域关联参数。                                                                                                           |
| [**WDI\_TLV\_FT\_REASSOC\_PARAMETERS**](wdi-tlv-ft-reassoc-parameters.md)                  |                                | X        | 快速转换参数 （MDIE，R0KH ID、 PMKR0Name，SNonce）。 这是仅存在可用于快速转换 （不在初始移动域关联）。 |
| [**WDI\_TLV\_BSS\_SELECTION\_PARAMETERS**](wdi-tlv-bss-selection-parameters.md)            |                                | X        | [**WDI\_BSS\_选择\_标志**](https://msdn.microsoft.com/library/windows/hardware/mt297629)提供 BSS 选择主机所使用的信息。                               |

 

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

 

 




