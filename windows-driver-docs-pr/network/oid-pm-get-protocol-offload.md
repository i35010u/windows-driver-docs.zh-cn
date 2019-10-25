---
title: OID_PM_GET_PROTOCOL_OFFLOAD
description: 过量驱动程序发出 OID_PM_GET_PROTOCOL_OFFLOAD 的 OID 方法请求，以获取来自网络适配器的低功率协议卸载的参数设置。
ms.assetid: c14b9278-6f24-41a1-bc2e-536a75460ecd
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_PM_GET_PROTOCOL_OFFLOAD 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: f3b6b3325b789bd23437c94af80df3fe1f8a9e01
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844058"
---
# <a name="oid_pm_get_protocol_offload"></a>OID\_PM\_获取\_协议\_卸载


过量驱动程序发出 OID\_的 OID 方法请求\_获取\_协议\_卸载，以便从网络适配器中获取低功率协议卸载的参数设置。

[**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员最初包含指向 ULONG 协议卸载标识符的指针。 成功从 OID 方法请求返回后， **ndis\_OID\_请求**结构的**InformationBuffer**成员包含指向[**NDIS\_PM\_协议\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)结构的指针。

<a name="remarks"></a>备注
-------

NDIS 6.20 和更高版本的协议驱动程序使用 OID\_PM\_获取\_协议\_卸载方法 OID，以便从网络适配器中检索低功率协议卸载的参数设置。

信息缓冲区必须指向 ULONG 类型协议卸载标识符。 Ndis 在[ **\_协议**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)的**ProtocolOffloadId**\_成员中设置此协议卸载标识符，在 Ndis 发送以前的[OID\_PM\_添加\_协议时\_卸载结构\_](oid-pm-add-protocol-offload.md)将 OID 请求卸载到基础网络适配器。

微型端口驱动程序为请求返回以下状态代码之一：

<a href="" id="ndis-status-success"></a>成功的 NDIS\_状态\_  
已成功检索请求的数据。 信息缓冲区包含相应的 NDIS\_PM\_协议\_卸载结构。

<a href="" id="ndis-status-pending"></a>NDIS\_状态\_挂起  
请求正在等待完成。 最终状态代码和结果将传递给调用方的 OID 请求完成处理程序。

<a href="" id="ndis-status-invalid-parameter"></a>NDIS\_状态\_无效\_参数  
指定的协议卸载标识符无效。

<a href="" id="ndis-status-buffer-too-short"></a>NDIS\_状态\_缓存\_\_太短  
信息缓冲区太短。 NDIS 设置**数据。查询\_信息。** \_OID 中的 BytesNeeded 成员\_请求结构到所需的最小缓冲区大小。

<a href="" id="ndis-status-not-supported"></a>不\_支持 NDIS\_状态\_  
此微型端口驱动程序的 NDIS 版本低于6.20。

<a href="" id="ndis-status-failure"></a>\_故障时的 NDIS\_状态  
由于上述原因之外的原因，导致请求失败。

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
<td><p>在 NDIS 6.20 和更高版本中受支持。 对于微型端口驱动程序是必需的。 （请参见 "备注" 部分。）</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS\_PM\_协议\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)

[OID\_PM\_添加\_协议\_卸载](oid-pm-add-protocol-offload.md)

 

 




