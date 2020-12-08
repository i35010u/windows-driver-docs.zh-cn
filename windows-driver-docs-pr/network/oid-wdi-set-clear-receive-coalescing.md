---
title: OID_WDI_SET_CLEAR_RECEIVE_COALESCING
description: 主机使用 OID_WDI_SET_CLEAR_RECEIVE_COALESCING 来删除数据包合并的数据包筛选器。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_SET_CLEAR_RECEIVE_COALESCING 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 73249f52f8ab9f51f181c068348eebd6b69c5d66
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829407"
---
# <a name="oid_wdi_set_clear_receive_coalescing"></a>OID \_ WDI \_ 设置 \_ 清除 \_ 接收 \_ 合并


OID \_ WDI \_ SET \_ CLEAR \_ RECEIVE \_ 合并由主机用于删除数据包合并的数据包筛选器。

| 范围 | 设置序列化任务 | 正常执行时间 (秒)  |
|-------|--------------------------|---------------------------------|
| 端口  | 是                      | 1                               |

 

## <a name="set-property-parameters"></a>设置属性参数


| TLV                                                                                            | 允许多个 TLV 实例 | 可选 | 说明                         |
|------------------------------------------------------------------------------------------------|--------------------------------|----------|-------------------------------------|
| [**WDI \_ TLV \_ 设置 \_ 清除 \_ 接收 \_ 合并**](./wdi-tlv-set-clear-receive-coalescing.md) |                                |          | 要删除的数据包筛选器 ID。 |

 

## <a name="set-property-results"></a>设置属性结果


无其他数据。 标头中的数据足够了。

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
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Dot11wdi</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[OID \_ WDI \_ 设置 \_ 接收 \_ 合并](oid-wdi-set-receive-coalescing.md)

 

