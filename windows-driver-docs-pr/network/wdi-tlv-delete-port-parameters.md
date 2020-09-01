---
title: WDI_TLV_DELETE_PORT_PARAMETERS
description: WDI_TLV_DELETE_PORT_PARAMETERS 是包含 OID_WDI_TASK_DELETE_PORT 的参数的 TLV。
ms.assetid: F3DDECDC-1A92-4022-9E2C-780ED480172C
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_DELETE_PORT_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 646fc3a6139319155d520cd9db0803d48e81acd4
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89214286"
---
# <a name="wdi_tlv_delete_port_parameters"></a>WDI \_ TLV \_ 删除 \_ 端口 \_ 参数


WDI \_ tlv \_ 删除 \_ 端口 \_ 参数是一个 TLV，其中包含 [OID \_ WDI \_ TASK \_ DELETE \_ 端口](./oid-wdi-task-delete-port.md)的参数。

## <a name="tlv-type"></a>TLV 类型


0x2A

## <a name="length"></a>Length


Sum (所有包含的元素的大小) 。

## <a name="values"></a>值


| 类型   | 说明                          |
|--------|--------------------------------------|
| UINT16 | 指定要删除的端口号。 |

 

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

 

