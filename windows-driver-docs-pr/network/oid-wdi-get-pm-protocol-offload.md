---
title: OID_WDI_GET_PM_PROTOCOL_OFFLOAD
description: OID_WDI_GET_PM_PROTOCOL_OFFLOAD 请求的协议列表将电源管理的卸载。
ms.assetid: ed7604fa-666c-4aa1-9041-ed56d282c29b
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_GET_PM_PROTOCOL_OFFLOAD 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: bcf76fc7b72c98e94625216dcdfb2a1f5a2b43d4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545251"
---
# <a name="oidwdigetpmprotocoloffload"></a>OID\_WDI\_GET\_PM\_PROTOCOL\_OFFLOAD


OID\_WDI\_获取\_PM\_协议\_卸载请求的协议列表将电源管理的卸载。

| 范围 | 设置与任务序列化 | 正常执行时间 （秒） |
|-------|--------------------------|---------------------------------|
| 端口  | 不适用           | 1                               |

 

## <a name="get-property-parameters"></a>获取属性参数


| TLV                                                                                  | 允许多个 TLV 实例 | 可选 | 描述          |
|--------------------------------------------------------------------------------------|--------------------------------|----------|----------------------|
| [**WDI\_TLV\_PM\_PROTOCOL\_OFFLOAD\_GET**](https://msdn.microsoft.com/library/windows/hardware/dn898034) |                                |          | 协议卸载 id。 |

 

## <a name="get-property-results"></a>获取属性的结果


| TLV                                                                                                         | 允许多个 TLV 实例 | 可选 | 描述                            |
|-------------------------------------------------------------------------------------------------------------|--------------------------------|----------|----------------------------------------|
| [**WDI\_TLV\_PM\_PROTOCOL\_OFFLOAD\_IPv4ARP**](https://msdn.microsoft.com/library/windows/hardware/dn898035)                |                                | X        | IPv4 ARP 协议卸载参数。  |
| [**WDI\_TLV\_PM\_PROTOCOL\_OFFLOAD\_IPv6NS**](https://msdn.microsoft.com/library/windows/hardware/dn898036)                  |                                | X        | IPv6 NS 协议卸载参数。   |
| [**WDI\_TLV\_PM\_PROTOCOL\_OFFLOAD\_80211RSN\_REKEY**](https://msdn.microsoft.com/library/windows/hardware/dn898033) |                                | X        | 重新生成密钥 RSN 协议卸载参数。 |

 

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
<td>Dot11wdi.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[OID\_WDI\_SET\_ADD\_PM\_PROTOCOL\_OFFLOAD](oid-wdi-set-add-pm-protocol-offload.md)

[OID\_WDI\_SET\_REMOVE\_PM\_PROTOCOL\_OFFLOAD](oid-wdi-set-remove-pm-protocol-offload.md)

 

 




