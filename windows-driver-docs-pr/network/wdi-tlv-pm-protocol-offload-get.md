---
title: WDI_TLV_PM_PROTOCOL_OFFLOAD_GET
description: WDI_TLV_PM_PROTOCOL_OFFLOAD_GET 是包含 OID_WDI_GET_PM_PROTOCOL_OFFLOAD 的协议卸载 ID 的 TLV。
ms.assetid: 71BBAA8F-0EE3-4315-AEB1-E9FD394218AD
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_PM_PROTOCOL_OFFLOAD_GET 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: cef3a4660fdc7a9dcdafcdbdf193cc5ea3ca350a
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217199"
---
# <a name="wdi_tlv_pm_protocol_offload_get"></a>WDI \_ TLV \_ PM \_ 协议 \_ 卸载 \_ GET


WDI \_ tlv \_ PM \_ 协议 \_ 卸载 \_ GET 是一个 TLV，其中包含用于 [OID \_ WDI \_ 获取 \_ PM \_ 协议 \_ 卸载](./oid-wdi-get-pm-protocol-offload.md)的协议卸载 ID。

## <a name="tlv-type"></a>TLV 类型


0xA8

## <a name="length"></a>Length


UINT32) 的大小 (以字节为单位）。

## <a name="values"></a>值


| 类型   | 说明                                                                                                                                                                                                                                                                                                 |
|--------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT32 | 指定协议卸载 ID。 这是操作系统提供的用于标识卸载协议的值。 在 OS 向下发送添加请求或完成对过量驱动程序的请求之前，操作系统会将 ProtocolOffloadId 设置为在网络适配器上的协议卸载之间唯一的值。 |

 

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

 

