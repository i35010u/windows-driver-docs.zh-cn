---
title: WDI_TLV_BSS_ENTRY
description: WDI_TLV_BSS_ENTRY 是包含 BSS 输入信息的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_BSS_ENTRY 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: f54dc436f46f6d165aa05583a32f2b99262aff5c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797861"
---
# <a name="wdi_tlv_bss_entry"></a>WDI \_ TLV \_ BSS \_ 条目


WDI \_ tlv \_ bss \_ 条目是包含 BSS 条目信息的 tlv。

## <a name="tlv-type"></a>TLV 类型


0x8

## <a name="length"></a>长度


Sum (包含所有 TLVs 的大小的) 字节。

## <a name="values"></a>值


| 类型                                                                                      | 允许多个 TLV 实例 | 可选                                                                            | 说明                                                                                                                                                                                                                                                       |
|-------------------------------------------------------------------------------------------|--------------------------------|-------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI \_ TLV \_ BSSID**](wdi-tlv-bssid.md)                                                  |                                |                                                                                     | BSS 的 BSSID。                                                                                                                                                                                                                                             |
| [**WDI \_ TLV \_ 探测 \_ 响应 \_ 帧**](wdi-tlv-probe-response-frame.md)                  |                                | X                                                                                   | 探测响应帧。 如果未收到探测响应帧，则为空。                                                                                                                                                                            |
| [**WDI \_ TLV \_ 信标 \_ 帧**](wdi-tlv-beacon-frame.md)                                   |                                | X                                                                                   | 信号框架。 如果未收到信号，则为空。                                                                                                                                                                                                  |
| [**WDI \_ TLV \_ BSS \_ 输入 \_ 信号 \_ 信息**](wdi-tlv-bss-entry-signal-info.md)               |                                |                                                                                     | 信号信息 (收到 BSS 的信号强度和链接质量) 。                                                                                                                                                                                    |
| [**WDI \_ TLV \_ BSS \_ 条目 \_ 通道 \_ 信息**](wdi-tlv-bss-entry-channel-info.md)             |                                |                                                                                     | BSS 条目的逻辑通道号和带区 ID。                                                                                                                                                                                                         |
| [**WDI \_ TLV \_ BSS \_ 条目 \_ 设备 \_ 上下文**](wdi-tlv-bss-entry-device-context.md)         |                                | X                                                                                   | 有关对等的设备上下文。 此上下文是从 IHV 组件提供的，可用于存储 IHV 组件要维护的每个 BSS 进入状态。 为了避免生存期管理问题，IHV 组件不能在此字段中使用指针。 |
| [**WDI \_ TLV \_ BSS \_ 条目 \_ AGE \_ 信息**](wdi-tlv-bss-entry-age-info.md)                     |                                | X (注意：如果受 IHV 组件维护，则此 TLV 是必需的。 )  | 此 BSS 条目的时间信息，包括最近发现此项的时间戳。                                                                                                                                                  |
| [**WDI \_ TLV \_ P2P \_ 发现的 \_ 服务 \_ 条目**](wdi-tlv-p2p-discovered-service-entry.md) | X                              | X                                                                                   | 在远程设备上找到的服务列表，其中包括在发现请求指定 WDI \_ P2P \_ 服务 \_ 发现 \_ 类型 \_ \_ 作为发现类型的情况下使用汽油查询检索的服务信息。                                  |

 

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

 

 




