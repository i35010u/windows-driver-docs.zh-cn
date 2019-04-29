---
title: NDIS_STATUS_PM_OFFLOAD_REJECTED
description: NDIS_STATUS_PM_OFFLOAD_REJECTED 状态指示过量电源管理协议卸载被拒绝的驱动程序。
ms.assetid: 54922e70-2b56-4141-b79b-73418c7553e3
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_PM_OFFLOAD_REJECTED 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 9a40d53d133bf2adc2e2515b8a208f0efdea3621
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362968"
---
# <a name="ndisstatuspmoffloadrejected"></a>NDIS\_状态\_PM\_卸载\_已拒绝


NDIS\_状态\_PM\_卸载\_已拒绝状态指示为过量电源管理协议卸载被拒绝的驱动程序。

<a name="remarks"></a>备注
-------

NDIS 或微型端口驱动程序可以生成 NDIS\_状态\_PM\_卸载\_已拒绝状态指示当其中任何一个将删除已卸载的协议。 **StatusBuffer**的成员[ **NDIS\_状态\_指示**](https://msdn.microsoft.com/library/windows/hardware/ff567373)结构包含的协议卸载标识符的 ULONG已拒绝的协议卸载。 NDIS 提供中的协议卸载标识符**ProtocolOffloadId**的成员[ **NDIS\_PM\_协议\_卸载**](https://msdn.microsoft.com/library/windows/hardware/ff566760)结构。

NDIS 生成 NDIS\_状态\_PM\_卸载\_已拒绝状态指示必须从网络适配器中删除以前已卸载的协议时。 例如，NDIS 可能会删除以释放资源以进行更高的优先级协议卸载协议卸载。 NDIS 卸载已拒绝的协议卸载，但不会发送到其他绑定的绑定发送的状态指示。

微型端口驱动程序报告此状态指示拒绝以前接受的协议卸载。 例如，对于 WiFi WOL 案例，微型端口驱动程序必须发出 NDIS\_状态\_PM\_卸载\_已拒绝状态指示时 （由于特定于供应商支持 WOL 不需 PTK/GTK 旋转基础结构支持）。

对于使用基础结构元素来卸载协议以及在基础结构间漫游的无线网络适配器，就可以新基础结构元素可能不支持与前一个相同的功能。 在这种情况下，微型端口驱动程序可以向 NDIS，发出的状态指示，NDIS 将会发布 NDIS\_状态\_PM\_卸载\_拒绝特定错误代码。

WiFi 驱动程序可能会缓存本地协议卸载请求。 当驱动程序处理用于添加或删除协议卸载 OID 时，该驱动程序可以选择仅更新其本地缓存。 该驱动程序可以延迟的基础结构更新，直到收到[OID\_PM\_参数](https://msdn.microsoft.com/library/windows/hardware/ff569768)OID。

基础结构可能没有足够的资源来满足所有协议卸载。 在这种情况下，基础结构可以接受该协议的部分列表将卸载。 微型端口驱动程序完成 OID\_PM\_参数设置请求、 微型端口驱动程序必须进行 NDIS\_状态\_PM\_卸载\_的每个已拒绝状态指示协议将卸载 AP 拒绝。

例如，网络适配器可用于 AP 的代理 ARP 支持 ARP 卸载。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Version</p></td>
<td><p>支持 NDIS 6.20 及更高版本。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS\_PM\_协议\_卸载**](https://msdn.microsoft.com/library/windows/hardware/ff566760)

[**NDIS\_状态\_指示**](https://msdn.microsoft.com/library/windows/hardware/ff567373)

[OID\_PM\_PARAMETERS](https://msdn.microsoft.com/library/windows/hardware/ff569768)

 

 




