---
title: OID_PM_GET_PROTOCOL_OFFLOAD
description: 过量的驱动程序问题的 OID_PM_GET_PROTOCOL_OFFLOAD OID 方法请求，以获得参数设置为低能耗协议将从网络适配器的卸载。
ms.assetid: c14b9278-6f24-41a1-bc2e-536a75460ecd
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_PM_GET_PROTOCOL_OFFLOAD 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: cf74c8499161cb592988fe5b7b855334cf7d46a6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360798"
---
# <a name="oidpmgetprotocoloffload"></a>OID\_PM\_获取\_协议\_卸载


基础驱动程序发出 OID 方法请求的 OID\_PM\_获取\_协议\_卸载以获得参数设置为低能耗协议卸载网络适配器中。

**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构最初包含一个指向 ULONG 协议卸载标识符。 通过 OID 方法请求成功返回后**InformationBuffer**的成员**NDIS\_OID\_请求**结构包含一个指向[**NDIS\_PM\_协议\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)结构。

<a name="remarks"></a>备注
-------

NDIS 6.20 和更高版本的协议驱动程序使用 OID\_PM\_获取\_协议\_卸载从网络适配器的卸载方法来检索参数设置为低能耗协议的 OID。

信息缓冲区必须指向 ULONG 类型协议卸载标识符。 NDIS 中设置此协议卸载标识符**ProtocolOffloadId**的成员[ **NDIS\_PM\_协议\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)结构时 NDIS 发送之前[OID\_PM\_添加\_协议\_卸载](oid-pm-add-protocol-offload.md)OID 为基础的网络适配器的请求。

微型端口驱动程序返回请求的以下状态代码之一：

<a href="" id="ndis-status-success"></a>NDIS\_状态\_成功  
已成功检索到所请求的数据。 在信息缓冲区中包含相应的 NDIS\_PM\_协议\_卸载结构。

<a href="" id="ndis-status-pending"></a>NDIS\_状态\_PENDING  
请求正在等待完成。 最终状态代码和结果将传递给调用方的 OID 请求完成处理程序。

<a href="" id="ndis-status-invalid-parameter"></a>NDIS\_状态\_无效\_参数  
指定的协议卸载标识符无效。

<a href="" id="ndis-status-buffer-too-short"></a>NDIS\_状态\_缓冲区\_过\_短  
信息缓冲区太短。 NDIS 集**数据。查询\_信息。BytesNeeded** NDIS 中的成员\_OID\_结构到最小缓冲区大小的请求是必需的。

<a href="" id="ndis-status-not-supported"></a>NDIS\_状态\_不\_支持  
微型端口驱动程序的 NDIS 版本低于 6.20。

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
<td><p>Version</p></td>
<td><p>支持 NDIS 6.20 及更高版本。 对于微型端口驱动程序是必需的。 （请参见备注部分。）</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS\_PM\_协议\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)

[OID\_PM\_添加\_协议\_卸载](oid-pm-add-protocol-offload.md)

 

 




