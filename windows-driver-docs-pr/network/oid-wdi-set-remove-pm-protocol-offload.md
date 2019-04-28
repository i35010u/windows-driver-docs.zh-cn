---
title: OID_WDI_SET_REMOVE_PM_PROTOCOL_OFFLOAD
description: OID_WDI_SET_REMOVE_PM_PROTOCOL_OFFLOAD 删除协议卸载由协议指定卸载 id。
ms.assetid: 47850c43-4d10-48f5-b2e9-1f94f23eabf2
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_SET_REMOVE_PM_PROTOCOL_OFFLOAD 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: cd9b833495e236c3a542f98495f9eb840504a06c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348696"
---
# <a name="oidwdisetremovepmprotocoloffload"></a>OID\_WDI\_SET\_REMOVE\_PM\_PROTOCOL\_OFFLOAD


OID\_WDI\_设置\_删除\_PM\_协议\_卸载中删除协议卸载由协议指定卸载 id。

| 范围 | 设置与任务序列化 | 正常执行时间 （秒） |
|-------|--------------------------|---------------------------------|
| 端口  | 是                      | 1                               |

 

## <a name="set-property-parameters"></a>设置属性参数


| TLV                                                                                        | 允许多个 TLV 实例 | 可选 | 描述          |
|--------------------------------------------------------------------------------------------|--------------------------------|----------|----------------------|
| [**WDI\_TLV\_PM\_PROTOCOL\_OFFLOAD\_REMOVE**](https://msdn.microsoft.com/library/windows/hardware/dn898037) |                                |          | 协议卸载 id。 |

 

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


[OID\_WDI\_GET\_PM\_PROTOCOL\_OFFLOAD](oid-wdi-get-pm-protocol-offload.md)

[OID\_WDI\_SET\_ADD\_PM\_PROTOCOL\_OFFLOAD](oid-wdi-set-add-pm-protocol-offload.md)

 

 




