---
title: OID_WDI_SET_REMOVE_WOL_PATTERN
description: OID_WDI_SET_REMOVE_WOL_PATTERN 从固件中删除 LAN 唤醒 (WOL) 模式。
ms.assetid: 9fb03747-b585-4c73-b004-1bdc2a995e9d
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_SET_REMOVE_WOL_PATTERN 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: f7bfc9d7db72f3d0caf8cdd1748ed0bc09929bf3
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89213247"
---
# <a name="oid_wdi_set_remove_wol_pattern"></a>OID \_ WDI \_ SET \_ 删除 \_ WOL \_ 模式


OID \_ WDI \_ SET \_ 删除 \_ WOL \_ 模式从固件中删除 LAN 唤醒 (wol) 模式。

| 作用域 | 设置序列化任务 | 正常执行时间 (秒)  |
|-------|--------------------------|---------------------------------|
| 端口  | 是                      | 1                               |

 

## <a name="set-property-parameters"></a>设置属性参数


| TLV                                                                                        | 允许多个 TLV 实例 | 可选 | 说明     |
|--------------------------------------------------------------------------------------------|--------------------------------|----------|-----------------|
| [**WDI \_ TLV \_ 唤醒 \_ 包 \_ 模式 \_ 删除**](./wdi-tlv-wake-packet-pattern-remove.md) |                                |          | WOL 模式 ID。 |

 

## <a name="set-property-results"></a>设置属性结果


无其他参数。 标头中的数据足够了。

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
<td>Dot11wdi</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[OID \_ WDI \_ 设置 \_ 添加 \_ WOL \_ 模式](oid-wdi-set-add-wol-pattern.md)

 

