---
title: WDI_TLV_DEFAULT_TX_KEY_ID_PARAMETERS
description: WDI_TLV_DEFAULT_TX_KEY_ID_PARAMETERS 是一个 TLV，其中包含用于 OID_WDI_SET_DEFAULT_KEY_ID 的端口上的数据包传输的默认密钥 ID。
ms.assetid: 24E7E758-FEED-4D2A-BAA8-6DBC08726FBA
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_DEFAULT_TX_KEY_ID_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 8e24259fb04ff649503b27bcc8133cae22c77535
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89213121"
---
# <a name="wdi_tlv_default_tx_key_id_parameters"></a>WDI \_ TLV \_ 默认 \_ TX \_ 密钥 \_ ID \_ 参数


WDI \_ tlv \_ 默认 \_ TX \_ 密钥 \_ ID \_ 参数是一个 TLV，其中包含用于 [OID \_ WDI \_ 设置 \_ 默认 \_ 密钥 \_ id](./oid-wdi-set-default-key-id.md)的端口上用于数据包传输的默认密钥 id。

## <a name="tlv-type"></a>TLV 类型


0x54

## <a name="length"></a>Length


UINT32) 的大小 (以字节为单位）。

## <a name="values"></a>值


| 类型   | 说明                                                     |
|--------|-----------------------------------------------------------------|
| UINT32 | 为端口上的数据包传输指定默认密钥 ID。 |

 

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

 

