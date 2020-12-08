---
title: WDI_TLV_PM_PROTOCOL_OFFLOAD_80211RSN_REKEY
description: WDI_TLV_PM_PROTOCOL_OFFLOAD_80211RSN_REKEY 是包含 RSN Rekey 协议卸载参数的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_PM_PROTOCOL_OFFLOAD_80211RSN_REKEY 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 4e00561cf253819c808833fe35b3d8b80e7fd791
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818059"
---
# <a name="wdi_tlv_pm_protocol_offload_80211rsn_rekey"></a>WDI \_ TLV \_ PM \_ 协议 \_ 卸载 \_ 80211RSN \_ REKEY


WDI \_ tlv \_ PM \_ 协议 \_ 卸载 \_ 80211RSN \_ rekey 是包含 RSN REKEY 协议卸载参数的 tlv。 如果配置了 TCK/iGTK 密钥信息，则驱动程序必须在通过此 TLV 在 [OID_WDI_GET_PM_PROTOCOL_OFFLOAD](oid-wdi-get-pm-protocol-offload.md) 中查询时将其返回。

## <a name="tlv-type"></a>TLV 类型


0x63

## <a name="length"></a>长度


Sum (所有包含的元素的大小) 。

## <a name="values"></a>值


| 类型 | 描述  |
| --- | --- |
| [WDI_TLV_RSN_KEY_INFO](wdi-tlv-rsn-key-info.md) | Rsn Eapol 密钥参数。 |
| 列出<[WDI_TLV_CONFIGURED_CIPHER_KEY](wdi-tlv-configured-cipher-key.md)> | 要在 [OID_WDI_GET_PM_PROTOCOL_OFFLOAD](oid-wdi-get-pm-protocol-offload.md)中设置的已配置密码的列表。 驱动程序必须返回当前配置的任何 GTK 或 iGTK 键。 |

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

 

 




