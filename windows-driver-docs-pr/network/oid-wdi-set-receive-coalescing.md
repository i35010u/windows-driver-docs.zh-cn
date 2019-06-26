---
title: OID_WDI_SET_RECEIVE_COALESCING
description: 主机使用 OID_WDI_SET_RECEIVE_COALESCING 添加数据包合并的数据包筛选器。
ms.assetid: c8856813-0d81-4735-95cc-d9b5dc6ede87
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_SET_RECEIVE_COALESCING 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 031fb37ae82bf68d4149c89839d1951c5c1a2d9c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359168"
---
# <a name="oidwdisetreceivecoalescing"></a>OID\_WDI\_SET\_RECEIVE\_COALESCING


OID\_WDI\_设置\_接收\_主机使用 COALESCING 添加数据包合并的数据包筛选器。

| 范围 | 设置与任务序列化 | 正常执行时间 （秒） |
|-------|--------------------------|---------------------------------|
| Port  | 是                      | 1                               |

 

当主机收到请求时从操作系统设置数据包合并筛选器时，它将使用此命令来添加数据包合并的数据包筛选器。 若要清除的数据包合并的数据包筛选器，请参阅[OID\_WDI\_设置\_清除\_接收\_COALESCING](oid-wdi-set-clear-receive-coalescing.md)。

## <a name="set-property-parameters"></a>设置属性参数


| TLV                                                                               | 允许多个 TLV 实例 | 可选 | 描述                                 |
|-----------------------------------------------------------------------------------|--------------------------------|----------|---------------------------------------------|
| [**WDI\_TLV\_SET\_RECEIVE\_COALESCING**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-set-receive-coalescing) |                                |          | 要设置的数据包合并参数。 |

 

## <a name="set-property-results"></a>设置属性结果


任何其他参数。 标头中的数据就足够了。

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
<td>Dot11wdi.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[OID\_WDI\_SET\_CLEAR\_RECEIVE\_COALESCING](oid-wdi-set-clear-receive-coalescing.md)

 

 




