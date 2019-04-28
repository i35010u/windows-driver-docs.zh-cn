---
title: OID_WDI_SET_ADD_PM_PROTOCOL_OFFLOAD
description: OID_WDI_SET_ADD_PM_PROTOCOL_OFFLOAD 将添加一个或多个协议的列表将电源管理的卸载。
ms.assetid: 50c69dd4-352d-484f-81c1-a4c9587ab368
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_SET_ADD_PM_PROTOCOL_OFFLOAD 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 1fd1db45482274a5c30993f4e4dd7900e42770d3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331227"
---
# <a name="oidwdisetaddpmprotocoloffload"></a>OID\_WDI\_SET\_ADD\_PM\_PROTOCOL\_OFFLOAD


OID\_WDI\_设置\_添加\_PM\_协议\_卸载将添加一个或多个协议的列表将电源管理的卸载。

| 范围 | 设置与任务序列化 | 正常执行时间 （秒） |
|-------|--------------------------|---------------------------------|
| 端口  | 是                      | 1                               |

 

此属性提供信息来启用设备/固件主 CPU 处于睡眠状态时实现这些协议。 在此状态的固件和设备处理的卸载的任务而无需唤醒主机。

## <a name="set-property-parameters"></a>设置属性参数


| TLV                                                                                                         | 允许多个 TLV 实例 | 可选 | 描述                            |
|-------------------------------------------------------------------------------------------------------------|--------------------------------|----------|----------------------------------------|
| [**WDI\_TLV\_PM\_PROTOCOL\_OFFLOAD\_IPv4ARP**](https://msdn.microsoft.com/library/windows/hardware/dn898035)                |                                | X        | IPv4 ARP 协议卸载参数。  |
| [**WDI\_TLV\_PM\_PROTOCOL\_OFFLOAD\_IPv6NS**](https://msdn.microsoft.com/library/windows/hardware/dn898036)                  |                                | X        | IPv6 NS 协议卸载参数。   |
| [**WDI\_TLV\_PM\_PROTOCOL\_OFFLOAD\_80211RSN\_REKEY**](https://msdn.microsoft.com/library/windows/hardware/dn898033) |                                | X        | 重新生成密钥 RSN 协议卸载参数。 |

 

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


[OID\_WDI\_GET\_PM\_PROTOCOL\_OFFLOAD](oid-wdi-get-pm-protocol-offload.md)

[OID\_WDI\_SET\_REMOVE\_PM\_PROTOCOL\_OFFLOAD](oid-wdi-set-remove-pm-protocol-offload.md)

 

 




