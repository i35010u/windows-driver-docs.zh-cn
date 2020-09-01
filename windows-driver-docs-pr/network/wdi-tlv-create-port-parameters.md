---
title: WDI_TLV_CREATE_PORT_PARAMETERS
description: WDI_TLV_CREATE_PORT_PARAMETERS 是包含 OID_WDI_TASK_CREATE_PORT 的参数的 TLV。
ms.assetid: CE0ACE11-5E7A-43E1-BE0B-8BA8F7FF8432
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_CREATE_PORT_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 08a70f8b1a1bafefffcac30903d2f09a93a07d7d
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89214298"
---
# <a name="wdi_tlv_create_port_parameters"></a>WDI \_ TLV \_ 创建 \_ 端口 \_ 参数


WDI \_ tlv \_ CREATE \_ 端口 \_ 参数是一个 TLV，其中包含 [OID \_ WDI \_ TASK \_ CREATE \_ 端口](./oid-wdi-task-create-port.md)的参数。

## <a name="tlv-type"></a>TLV 类型


0x28

## <a name="length"></a>Length


Sum (所有包含的元素的大小) 。

## <a name="values"></a>值


| 类型   | 说明                                                                                                                                                                             |
|--------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT16 | 主机可以在正在创建的端口上配置的操作模式的按位 "或" 值。 操作模式在 [**WDI \_ 操作 \_ 模式下**](/windows-hardware/drivers/ddi/dot11wdi/ne-dot11wdi-_wdi_operation_mode)定义。 |
| UINT32 | \_ \_ 将与所创建端口关联的 NDIS 端口号。 除非适配器要处理非 WDI 的 Oid，否则不需要对此字段执行任何操作。                 |

 

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

 

