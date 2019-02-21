---
title: WDI_TLV_PM_PROTOCOL_OFFLOAD_80211RSN_REKEY
description: WDI_TLV_PM_PROTOCOL_OFFLOAD_80211RSN_REKEY 是 TLV 包含 RSN 重新生成密钥协议卸载参数。
ms.assetid: 4FDB56EA-444B-4EA2-B8D1-5E740734EEED
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_PM_PROTOCOL_OFFLOAD_80211RSN_REKEY 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 72033a9acd362cc10e77814e659e3b8ef8a92d8c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545368"
---
# <a name="wditlvpmprotocoloffload80211rsnrekey"></a>WDI\_TLV\_PM\_PROTOCOL\_OFFLOAD\_80211RSN\_REKEY


WDI\_TLV\_PM\_协议\_卸载\_80211RSN\_重新生成密钥是包含 RSN 重新生成密钥协议卸载参数 TLV。 如果配置 TCK/iGTK 在密钥信息，驱动程序必须返回它在查询时[OID_WDI_GET_PM_PROTOCOL_OFFLOAD](oid-wdi-get-pm-protocol-offload.md)此 TLV 通过。

## <a name="tlv-type"></a>TLV 类型


0x63

## <a name="length"></a>长度


所有包含的元素的大小的总和 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入 | 描述  |
| --- | --- |
| [WDI_TLV_RSN_KEY_INFO](wdi-tlv-rsn-key-info.md) | Rsn Eapol 键参数。 |
| LIST<[WDI_TLV_CONFIGURED_CIPHER_KEY](wdi-tlv-configured-cipher-key.md)> | 配置密码中设置的列表[OID_WDI_GET_PM_PROTOCOL_OFFLOAD](oid-wdi-get-pm-protocol-offload.md)。 驱动程序必须返回当前配置的任何 GTK 或 iGTK 键。 |

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

 

 




