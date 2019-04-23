---
title: OID_WDI_SET_RECEIVE_COALESCING
description: 主机使用 OID_WDI_SET_RECEIVE_COALESCING 添加数据包合并的数据包筛选器。
ms.assetid: c8856813-0d81-4735-95cc-d9b5dc6ede87
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_SET_RECEIVE_COALESCING 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 88328276655a68a71fa2ab013a9b271e70f363ba
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59902343"
---
# <a name="oidwdisetreceivecoalescing"></a>OID\_WDI\_SET\_RECEIVE\_COALESCING


OID\_WDI\_设置\_接收\_主机使用 COALESCING 添加数据包合并的数据包筛选器。

| 范围 | 设置与任务序列化 | 正常执行时间 （秒） |
|-------|--------------------------|---------------------------------|
| 端口  | 是                      | 1                               |

 

当主机收到请求时从操作系统设置数据包合并筛选器时，它将使用此命令来添加数据包合并的数据包筛选器。 若要清除的数据包合并的数据包筛选器，请参阅[OID\_WDI\_设置\_清除\_接收\_COALESCING](oid-wdi-set-clear-receive-coalescing.md)。

## <a name="set-property-parameters"></a>设置属性参数


| TLV                                                                               | 允许多个 TLV 实例 | 可选 | 描述                                 |
|-----------------------------------------------------------------------------------|--------------------------------|----------|---------------------------------------------|
| [**WDI\_TLV\_SET\_RECEIVE\_COALESCING**](https://msdn.microsoft.com/library/windows/hardware/dn898061) |                                |          | 要设置的数据包合并参数。 |

 

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

 

 




