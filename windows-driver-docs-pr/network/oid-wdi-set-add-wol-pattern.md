---
title: OID_WDI_SET_ADD_WOL_PATTERN
description: OID_WDI_SET_ADD_WOL_PATTERN 向固件的 LAN 唤醒 (WOL) 模式。
ms.assetid: 96fb71fd-412b-4013-b3bc-c31a43516f55
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_SET_ADD_WOL_PATTERN 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 4def5ce6b4796889502ae2ab3bf5551026063578
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59902971"
---
# <a name="oidwdisetaddwolpattern"></a>OID\_WDI\_SET\_ADD\_WOL\_PATTERN


OID\_WDI\_设置\_添加\_WOL\_模式将 LAN 唤醒 (WOL) 模式添加到固件。

| 范围 | 设置与任务序列化 | 正常执行时间 （秒） |
|-------|--------------------------|---------------------------------|
| 端口  | 是                      | 1                               |

 

主机定义要添加到固件的数据包模式类型。 固件 Dx 中检测到匹配的数据包到达。 如果检测到，固件断言唤醒中断。

## <a name="set-property-parameters"></a>设置属性参数


| TLV                                                                                                              | 允许多个 TLV 实例 | 可选 | 描述                                   |
|------------------------------------------------------------------------------------------------------------------|--------------------------------|----------|-----------------------------------------------|
| [**WDI\_TLV\_WAKE\_PACKET\_BITMAP\_PATTERN**](https://msdn.microsoft.com/library/windows/hardware/dn898084)                       | X                              | X        | WOL 模式信息。                      |
| [**WDI\_TLV\_WAKE\_PACKET\_MAGIC\_PACKET**](https://msdn.microsoft.com/library/windows/hardware/dn898185)                           |                                | X        | 模式的幻数据包的 ID。               |
| [**WDI\_TLV\_WAKE\_PACKET\_IPv4\_TCP\_SYNC**](https://msdn.microsoft.com/library/windows/hardware/dn898089)                        | X                              | X        | WOL IPv4 TCP 同步数据包信息。         |
| [**WDI\_TLV\_WAKE\_PACKET\_IPv6\_TCP\_SYNC**](https://msdn.microsoft.com/library/windows/hardware/dn898091)                        | X                              | X        | WOL IPv4 TCP 同步数据包信息。         |
| [**WDI\_TLV\_WAKE\_PACKET\_EAPOL\_REQUEST\_ID\_MESSAGE**](https://msdn.microsoft.com/library/windows/hardware/dn898087) |                                | X        | WOL EAPOL 请求 ID 消息模式 ID。 |

 

## <a name="set-property-results"></a>设置属性结果


没有其他数据。 标头中的数据就足够了。

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


[OID\_WDI\_SET\_REMOVE\_WOL\_PATTERN](oid-wdi-set-remove-wol-pattern.md)

 

 




