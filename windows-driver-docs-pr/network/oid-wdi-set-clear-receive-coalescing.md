---
title: OID_WDI_SET_CLEAR_RECEIVE_COALESCING
description: OID_WDI_SET_CLEAR_RECEIVE_COALESCING 主机用于删除数据包合并的数据包筛选器。
ms.assetid: 1c2848c4-c412-4f33-9fc6-bf900a89c65d
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_SET_CLEAR_RECEIVE_COALESCING 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: bd0172db3f03d96a1897d671e85c986559aba64d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521471"
---
# <a name="oidwdisetclearreceivecoalescing"></a>OID\_WDI\_SET\_CLEAR\_RECEIVE\_COALESCING


OID\_WDI\_设置\_清除\_接收\_主机使用 COALESCING 若要删除数据包合并的数据包筛选器。

| 范围 | 设置与任务序列化 | 正常执行时间 （秒） |
|-------|--------------------------|---------------------------------|
| 端口  | 是                      | 1                               |

 

## <a name="set-property-parameters"></a>设置属性参数


| TLV                                                                                            | 允许多个 TLV 实例 | 可选 | 描述                         |
|------------------------------------------------------------------------------------------------|--------------------------------|----------|-------------------------------------|
| [**WDI\_TLV\_SET\_CLEAR\_RECEIVE\_COALESCING**](https://msdn.microsoft.com/library/windows/hardware/dn898057) |                                |          | 要删除的数据包筛选器 ID。 |

 

## <a name="set-property-results"></a>设置属性结果


没有其他数据。 标头中的数据就足够了。
要求
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
<td>Dot11wdi.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[OID\_WDI\_SET\_RECEIVE\_COALESCING](oid-wdi-set-receive-coalescing.md)

 

 




