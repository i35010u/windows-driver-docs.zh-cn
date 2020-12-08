---
title: WDI_TLV_CONNECT_BSS_ENTRY
description: WDI_TLV_CONNECT_BSS_ENTRY 是包含候选连接 BSS 条目列表的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_CONNECT_BSS_ENTRY 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 732837acc76a97c07ee39669670d2c918b3ad58a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807983"
---
# <a name="wdi_tlv_connect_bss_entry"></a>WDI \_ TLV \_ 连接 \_ BSS \_ 条目


WDI \_ tlv \_ 连接 \_ bss \_ 项是一个 TLV，其中包含候选连接 BSS 条目的列表。

## <a name="tlv-type"></a>TLV 类型


0x34

## <a name="length"></a>长度


Sum (包含所有 TLVs 的大小的) 字节。

## <a name="values"></a>值


| 类型                                                                                        | 允许多个 TLV 实例 | 可选 | 说明                                                                                                                                                   |
|---------------------------------------------------------------------------------------------|--------------------------------|----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI \_ TLV \_ BSSID**](wdi-tlv-bssid.md)                                                    |                                |          | BSS 的 BSSID。                                                                                                                                         |
| [**WDI \_ TLV \_ 探测 \_ 响应 \_ 帧**](wdi-tlv-probe-response-frame.md)                    |                                | X        | 探测响应帧。 如果未收到探测响应，则为空。                                                                        |
| [**WDI \_ TLV \_ 信标 \_ 帧**](wdi-tlv-beacon-frame.md)                                     |                                | X        | 信号框架。 如果未收到信号，则为空。                                                                                        |
| [**WDI \_ TLV \_ BSS \_ 输入 \_ 信号 \_ 信息**](wdi-tlv-bss-entry-signal-info.md)                 |                                |          | 此 BSS 条目的信号信息。                                                                                                                    |
| [**WDI \_ TLV \_ BSS \_ 条目 \_ 通道 \_ 信息**](wdi-tlv-bss-entry-channel-info.md)               |                                |          | 此 BSS 条目的通道信息。                                                                                                                   |
| [**WDI \_ TLV \_ BSS \_ 条目 \_ 设备 \_ 上下文**](wdi-tlv-bss-entry-device-context.md)           |                                | X        | IHV 提供有关此对等方的上下文数据。                                                                                                                |
| [**WDI \_ TLV \_ PMKID**](wdi-tlv-pmkid.md)                                                    |                                | X        | 此 BSS 条目的16字节 PMKID 值。                                                                                                                   |
| [**WDI \_ TLV \_ 额外 \_ 关联 \_ 请求 \_**](wdi-tlv-extra-association-request-ies.md) |                                | X        | 要包含在 (中的 IE) 此 BSSID 的关联请求框架。 如果存在，则除了常见的 IE 外，还应包括此项。                  |
| [**WDI \_ TLV \_ FT \_ 初始 \_ ASSOC \_ 参数**](wdi-tlv-ft-initial-assoc-parameters.md)     |                                | X        | 初始移动域关联参数。                                                                                                           |
| [**WDI \_ TLV \_ FT \_ REASSOC \_ 参数**](wdi-tlv-ft-reassoc-parameters.md)                  |                                | X        | Fast 转换参数 (MDIE，R0KH，PMKR0Name，SNonce) 。 这仅适用于快速转换 (在初始移动域关联) 期间。 |
| [**WDI \_ TLV \_ TLV \_ 选择 \_ 参数**](wdi-tlv-bss-selection-parameters.md)            |                                | X        | [**WDI \_提供 \_ \_**](/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_bss_selection_flags) 主机用于 BSS 选择的信息的 BSS 选择标志。                               |

 

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

 

