---
title: OID_TCP_RSC_STATISTICS
description: 为查询，NDIS 和基础驱动程序或用户模式应用程序使用 OID_TCP_RSC_STATISTICS OID 获取接收段合并 (RSC) 统计信息的微型端口适配器。
ms.assetid: CD289868-1925-4222-8A4D-359118124325
ms.date: 08/08/2017
keywords: -OID_TCP_RSC_STATISTICS 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: fe48b97ade31b80a5e424b90d6358f3f1290f628
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354145"
---
# <a name="oidtcprscstatistics"></a>OID\_TCP\_RSC\_统计信息


为查询，NDIS 和基础驱动程序或用户模式应用程序使用 OID\_TCP\_RSC\_统计信息 OID 获取接收段合并 (RSC) 统计信息的微型端口适配器。

NDIS 6.30 和更高版本的微型端口驱动程序提供 RSC 服务必须支持此 OID。 否则，此 OID 是可选的。

<a name="remarks"></a>备注
-------

**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含[ **NDIS\_RSC\_统计信息\_信息**](https://msdn.microsoft.com/library/windows/hardware/hh451657)结构。

微型端口驱动程序必须维护中的成员的统计信息[ **NDIS\_RSC\_统计信息\_信息**](https://msdn.microsoft.com/library/windows/hardware/hh451657)结构，如下所示：

-   该驱动程序必须递增中的合并的数据包数**CoalescedPkts**由一个每次数据包添加到单个合并单元 (SCU) 的成员。
-   该驱动程序必须递增中的合并后的八位字节计数**CoalescedOctets**成员的每次数据包添加到 SCU 数据包的 TCP 有效负载大小。
-   该驱动程序必须递增合并的事件数**CoalesceEvents**由一个每次完成 SCU 的成员。 所有此类 SCUs 应具有一个非零**CoalescedSegCount**值。
-   该驱动程序必须递增中的中止计数**中止**每次它遇到的异常不是 IP 数据报长度超过一个的成员。 此计数应包括数据包由于硬件资源的未合并其中的用例。

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
<td><p>NDIS 6.30 和更高版本在 Windows 8 中的驱动程序支持。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS\_OID\_REQUEST**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NDIS\_RSC\_STATISTICS\_INFO**](https://msdn.microsoft.com/library/windows/hardware/hh451657)

 

 




