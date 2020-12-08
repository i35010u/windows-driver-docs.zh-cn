---
title: WDI_TLV_BSSID_INFO
description: WDI_TLV_BSSID_INFO 是包含 BSSID 信息的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_BSSID_INFO 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 8e2da7a173d0c6e9ce0db356574185fa20fa6059
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827471"
---
# <a name="wdi_tlv_bssid_info"></a>WDI \_ TLV \_ BSSID \_ 信息


WDI \_ tlv \_ bssid \_ 信息是包含 BSSID 信息的 tlv。

## <a name="tlv-type"></a>TLV 类型


0x120

## <a name="length"></a>长度


Sum (所有包含的元素的大小) 。

## <a name="values"></a>值


| 类型  | 描述                                                                                                                                                                                                                                                                                                                               |
|-------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT8 | AP 可访问性。 有效值为 1 (无法访问) 、2 (未知) 和 3 (可访问的) 。                                                                                                                                                                                                                                                      |
| UINT8 | 安全性。 如果此项设置为1，则表示此 BSSID 标识的 AP 支持与当前关联中的 STA 所使用的相同安全设置。 如果此设置为0，则表示此 AP 不支持相同的安全设置，或者安全信息目前不可用。 |
| UINT8 | 键范围位。 如果将其设置为1，则表示此 BSSID 指示的 AP 与发送报表的 AP 具有相同的身份验证器。 如果此位设置为0，则表示不同的身份验证器或信息不可用。                                                                                                |
| UINT8 | 如果 dot11SpectrumManagementRequired 为 true，则此值设置为1。                                                                                                                                                                                                                                                                              |
| UINT8 | 如果 dot11QosOptionImplemented 为 true，则此值设置为1。                                                                                                                                                                                                                                                                                    |
| UINT8 | 如果 dot11APSDOptionImplemented 为 true，则 AP 将 APSD 子字段设置为1，否则将其设置为0。                                                                                                                                                                                            |
| UINT8 | 如果 dot11RadioMeasurementActivated 为 true，则此值设置为1。                                                                                                                                                                                                                                                                               |
| UINT8 | 如果 dot11DelayedBlockAckOptionImplemented 为 true，则此值设置为1。                                                                                                                                                                                                                                                                        |
| UINT8 | 如果 dot11ImmediateBlockAckOptionImplemented 为 true，则此值设置为1。                                                                                                                                                                                                                                                                      |
| UINT8 | 如果此 BSSID 表示的 AP 在其信标帧中包含 MDE，则此项设置为1。                                                                                                                                                                                                                                                |
| UINT8 | 此项设置为1，表示此 BSSID 表示的 AP 为 HT AP，其中包括其信号中的 HT 功能元素。                                                                                                                                                                                                      |

 

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

 

 




