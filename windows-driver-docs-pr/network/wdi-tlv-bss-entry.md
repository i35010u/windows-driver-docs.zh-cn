---
title: WDI_TLV_BSS_ENTRY
description: WDI_TLV_BSS_ENTRY 是 TLV 包含 BSS 条目信息。
ms.assetid: 1D3AAB94-9FCE-4243-994A-7195440DDFCA
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_BSS_ENTRY 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 17452b6d04ea66c8381c8c993d66d3c5fe8288d5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329891"
---
# <a name="wditlvbssentry"></a>WDI\_TLV\_BSS\_条目


WDI\_TLV\_BSS\_项是包含 BSS 条目信息 TLV。

## <a name="tlv-type"></a>TLV 类型


0x8

## <a name="length"></a>长度


所有的大小 （以字节为单位） 总和包含 TLVs。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                                                      | 允许多个 TLV 实例 | 可选                                                                            | 描述                                                                                                                                                                                                                                                       |
|-------------------------------------------------------------------------------------------|--------------------------------|-------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_BSSID**](wdi-tlv-bssid.md)                                                  |                                |                                                                                     | BSS BSSID。                                                                                                                                                                                                                                             |
| [**WDI\_TLV\_探测\_响应\_帧**](wdi-tlv-probe-response-frame.md)                  |                                | X                                                                                   | 探测响应帧。 如果不收到任何探测响应帧，这为空。                                                                                                                                                                            |
| [**WDI\_TLV\_BEACON\_FRAME**](wdi-tlv-beacon-frame.md)                                   |                                | X                                                                                   | 信号帧。 如果收到没有信号，则为空。                                                                                                                                                                                                  |
| [**WDI\_TLV\_BSS\_条目\_信号\_信息**](wdi-tlv-bss-entry-signal-info.md)               |                                |                                                                                     | BSS 信号信息 （接收到的信号强度和链接质量）。                                                                                                                                                                                    |
| [**WDI\_TLV\_BSS\_条目\_通道\_信息**](wdi-tlv-bss-entry-channel-info.md)             |                                |                                                                                     | BSS 项的逻辑的通道数量和带区 ID。                                                                                                                                                                                                         |
| [**WDI\_TLV\_BSS\_ENTRY\_DEVICE\_CONTEXT**](wdi-tlv-bss-entry-device-context.md)         |                                | X                                                                                   | 有关对等方的设备上下文。 此上下文从 IHV 组件提供，可用于存储 IHV 组件想要维护的每个 BSS 项状态。 若要避免生存期管理问题，IHV 组件必须在此字段中不使用指针。 |
| [**WDI\_TLV\_BSS\_ENTRY\_AGE\_INFO**](wdi-tlv-bss-entry-age-info.md)                     |                                | X (注意：此 TLV 是必需的如果由 IHV 组件维护 BSS 列表。） | 此 BSS 项，包括最新发现此条目的时间戳的年龄信息。                                                                                                                                                  |
| [**WDI\_TLV\_P2P\_已发现\_服务\_条目**](wdi-tlv-p2p-discovered-service-entry.md) | X                              | X                                                                                   | 如果发现请求指定 WDI 使用天然气查询包括的服务信息检索远程设备上找到的服务列表\_P2P\_服务\_发现\_类型\_服务\_发现类型的信息。                                  |

 

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

 

 




