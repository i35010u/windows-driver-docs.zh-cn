---
title: WDI_TLV_PM_PROTOCOL_OFFLOAD_REMOVE
description: WDI_TLV_PM_PROTOCOL_OFFLOAD_REMOVE 是一个 TLV，其中包含要在 OID_WDI_SET_REMOVE_PM_PROTOCOL_OFFLOAD 中删除的协议卸载 ID。
ms.assetid: BD74C9F7-6370-41D5-841F-6949D7748E30
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_PM_PROTOCOL_OFFLOAD_REMOVE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: c9841c102a79065f0f0e9fe962b02f96a1dc3577
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89207767"
---
# <a name="wdi_tlv_pm_protocol_offload_remove"></a>WDI \_ TLV \_ PM \_ 协议 \_ 卸载 \_ 删除


WDI \_ tlv \_ PM \_ 协议 \_ 卸载 \_ 删除是一个 TLV，其中包含要删除的包含的协议卸载 [ID \_ \_ \_ \_ \_ \_ ](./oid-wdi-set-remove-pm-protocol-offload.md)。

## <a name="tlv-type"></a>TLV 类型


0x6C

## <a name="length"></a>Length


UINT32) 的大小 (以字节为单位）。

## <a name="values"></a>值


| 类型   | 说明                        |
|--------|------------------------------------|
| UINT32 | 指定协议卸载 ID。 |

 

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

 

