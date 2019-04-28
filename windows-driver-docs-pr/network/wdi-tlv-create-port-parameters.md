---
title: WDI_TLV_CREATE_PORT_PARAMETERS
description: WDI_TLV_CREATE_PORT_PARAMETERS 是包含参数的 OID_WDI_TASK_CREATE_PORT TLV。
ms.assetid: CE0ACE11-5E7A-43E1-BE0B-8BA8F7FF8432
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_CREATE_PORT_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: a616c4e5f15aef28de73d8ad7581e6be39f8145f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331806"
---
# <a name="wditlvcreateportparameters"></a>WDI\_TLV\_创建\_端口\_参数


WDI\_TLV\_创建\_端口\_参数是包含参数的 TLV [OID\_WDI\_任务\_创建\_端口](https://msdn.microsoft.com/library/windows/hardware/dn925949).

## <a name="tlv-type"></a>TLV 类型


0x28

## <a name="length"></a>长度


所有包含的元素的大小的总和 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入   | 描述                                                                                                                                                                             |
|--------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT16 | 操作模式的按位 OR 值可能正在创建的端口上配置主机。 在中定义的操作模式[ **WDI\_操作\_模式**](https://msdn.microsoft.com/library/windows/hardware/dn926085)。 |
| UINT32 | NDIS\_端口\_将与创建的端口相关联的数量。 除非适配器想要处理非 WDI Oid，它不需要执行任何操作此字段。                 |

 

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
<td><p>Header</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




