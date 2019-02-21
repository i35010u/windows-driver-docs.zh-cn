---
title: OID_PM_ADD_PROTOCOL_OFFLOAD
description: 作为一组协议的 NDIS 驱动程序使用 OID_PM_ADD_PROTOCOL_OFFLOAD OID 将电源管理协议卸载添加到网络适配器。
ms.assetid: 418f4ce8-64af-4e1e-877a-4cc606f63747
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_PM_ADD_PROTOCOL_OFFLOAD 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: e04155e5118fd1971cdd753cba629235da9d1644
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555608"
---
# <a name="oidpmaddprotocoloffload"></a>OID\_PM\_添加\_协议\_卸载


作为一组协议的 NDIS 驱动程序使用 OID\_PM\_添加\_协议\_卸载 OID，若要将协议添加到的网络适配器的电源管理的卸载。 **InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含一个指向[ **NDIS\_PM\_协议\_卸载**](https://msdn.microsoft.com/library/windows/hardware/ff566760)结构。

<a name="remarks"></a>备注
-------

NDIS 6.20 和更高版本的协议驱动程序使用 OID\_PM\_添加\_协议\_卸载 OID，若要将协议添加到的网络适配器的电源管理的卸载。 如果请求成功，网络适配器必须生成并传输卸载协议的必要的响应数据包的网络适配器处于低功耗状态时。

已成功将绑定到基础的网络适配器，只要它具有所需的数据 （如接口的 IP 地址） 来卸载协议后，协议驱动程序可以卸载协议。 协议驱动程序还可以将卸载某些其他电源管理事件通知，例如以前添加的 WOL 模式或卸载的协议的拒绝响应中的协议。

若要避免争用条件在 NDIS 和其他协议驱动程序绑定到相同的微型端口适配器，NDIS 启动将网络适配器设置为低功耗状态后，将卸载到该网络适配器的另一种协议的任何尝试会失败。 例如，如果 NDIS 协议驱动程序尝试卸载处理的上下文中的协议**NetEventSetPower**为该网络适配器，NDIS 事件通知将会使请求失败。

NDIS 发送到基础的 NDIS 驱动程序此 OID 请求或对基础驱动程序的请求完成之前，它会设置 ULONG **ProtocolOffloadId**的成员[ **NDIS\_PM\_协议\_卸载**](https://msdn.microsoft.com/library/windows/hardware/ff566760)为唯一值的结构。 协议驱动程序和 NDIS 使用与此协议卸载标识符[OID\_PM\_删除\_协议\_卸载](oid-pm-remove-protocol-offload.md)OID 请求删除从协议卸载基础网络适配器。

**请注意**  协议卸载标识符是为每个网络适配器设置协议卸载的唯一值。 但是，协议卸载标识符不是全局唯一跨所有网络适配器。

 

如果 NDIS 或基础的网络适配器将拒绝卸载，它将生成[ **NDIS\_状态\_PM\_卸载\_已拒绝**](https://msdn.microsoft.com/library/windows/hardware/ff567412)状态指示。 这可能是返回 NDIS 后\_状态\_OID 的成功。 **StatusBuffer**的成员[ **NDIS\_状态\_指示**](https://msdn.microsoft.com/library/windows/hardware/ff567373)结构包含的 ULONG 协议卸载标识符拒绝协议卸载。

本机 802.11 无线 LAN 微端口驱动程序如何使用此 OID 的信息，请参阅[添加和删除低电源协议卸载](https://msdn.microsoft.com/library/windows/hardware/ff543707)。

微型端口驱动程序返回请求的以下状态代码之一：

<a href="" id="ndis-status-success"></a>NDIS\_状态\_成功  
请求的协议卸载已成功添加。 **ProtocolOffloadId**的成员[ **NDIS\_PM\_协议\_卸载**](https://msdn.microsoft.com/library/windows/hardware/ff566760)结构包含协议卸载标识符。

<a href="" id="ndis-status-pending"></a>NDIS\_状态\_PENDING  
请求正在等待完成。 NDIS 将传递的最终状态代码和结果到 OID 请求完成处理程序的调用方完成请求之后。

<a href="" id="ndis-status-pm-protocol-offload-list-full"></a>NDIS\_状态\_PM\_协议\_卸载\_列表\_完整  
请求失败，因为协议卸载列表已满，网络适配器不能添加另一个协议卸载。

<a href="" id="ndis-status-resources"></a>NDIS\_状态\_资源  
NDIS 或基础的网络适配器无法添加新的协议卸载，由于缺少资源。

<a href="" id="ndis-status-invalid-parameter"></a>NDIS\_状态\_无效\_参数  
中的一个或多个参数[ **NDIS\_PM\_协议\_卸载**](https://msdn.microsoft.com/library/windows/hardware/ff566760)结构无效。

<a href="" id="ndis-status-buffer-too-short"></a>NDIS\_状态\_缓冲区\_过\_短  
信息缓冲区太短。 NDIS 集**数据。设置\_信息。BytesNeeded** NDIS 中的成员\_OID\_结构到最小缓冲区大小的请求是必需的。

<a href="" id="ndis-status-not-supported"></a>NDIS\_状态\_不\_支持  
网络适配器不支持请求的协议卸载。

<a href="" id="ndis-status-failure"></a>NDIS\_状态\_失败  
请求失败，而原因并非前面的原因。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>支持 NDIS 6.20 及更高版本。 对于微型端口驱动程序是必需的。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS\_OID\_REQUEST**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NDIS\_PM\_协议\_卸载**](https://msdn.microsoft.com/library/windows/hardware/ff566760)

[**NDIS\_状态\_指示**](https://msdn.microsoft.com/library/windows/hardware/ff567373)

[**NDIS\_状态\_PM\_卸载\_已拒绝**](https://msdn.microsoft.com/library/windows/hardware/ff567412)

[OID\_PM\_删除\_协议\_卸载](oid-pm-remove-protocol-offload.md)

[添加和删除低能耗协议卸载](https://msdn.microsoft.com/library/windows/hardware/ff543707)

 

 




