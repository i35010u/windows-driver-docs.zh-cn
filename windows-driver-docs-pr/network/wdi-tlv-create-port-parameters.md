---
title: WDI_TLV_CREATE_PORT_PARAMETERS
description: WDI_TLV_CREATE_PORT_PARAMETERS 是一个 TLV，其中包含 OID_WDI_TASK_CREATE_PORT 的参数。
ms.assetid: CE0ACE11-5E7A-43E1-BE0B-8BA8F7FF8432
ms.date: 07/18/2017
keywords:
- WDI_TLV_CREATE_PORT_PARAMETERS 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 8ffab1a249624d2dfe89b6d2c07601bdf61a6ffa
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843384"
---
# <a name="wdi_tlv_create_port_parameters"></a>WDI\_TLV\_创建\_端口\_参数


WDI\_TLV\_创建\_端口\_参数是一个 TLV，其中包含 OID 的参数[\_WDI\_\_\_创建端口](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-create-port)。

## <a name="tlv-type"></a>TLV 类型


0x28

## <a name="length"></a>长度


所有包含的元素的大小的总和（以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入   | 描述                                                                                                                                                                             |
|--------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT16 | 主机可以在正在创建的端口上配置的操作模式的按位 "或" 值。 操作模式在[**WDI\_operation\_模式下**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ne-dot11wdi-_wdi_operation_mode)定义。 |
| UINT32 | NDIS\_端口将与创建的端口关联\_号。 除非适配器要处理非 WDI 的 Oid，否则不需要对此字段执行任何操作。                 |

 

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
<td><p>Windows 10</p></td>
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

 

 




