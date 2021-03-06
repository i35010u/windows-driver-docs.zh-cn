---
title: OID_PM_GET_PROTOCOL_OFFLOAD
description: 过量驱动程序发出 OID_PM_GET_PROTOCOL_OFFLOAD 的 OID 方法请求，以获取来自网络适配器的低功率协议卸载的参数设置。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_PM_GET_PROTOCOL_OFFLOAD 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: e9936073fd80a2e5a12820e362e4350c0b58cfb7
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102249024"
---
# <a name="oid_pm_get_protocol_offload"></a>OID \_ PM \_ 获取 \_ 协议 \_ 卸载


过量驱动程序发出 OID \_ PM 获取协议卸载的 oid 方法请求 \_ \_ \_ ，以便从网络适配器中获取低功率协议卸载的参数设置。

[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)结构的 **INFORMATIONBUFFER** 成员最初包含指向 ULONG 协议卸载标识符的指针。 成功从 OID 方法请求返回后， **ndis \_ OID \_ 请求** 结构的 **InformationBuffer** 成员包含指向 [**NDIS \_ PM \_ 协议 \_ 卸载**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)结构的指针。

<a name="remarks"></a>备注
-------

NDIS 6.20 和更高版本的协议驱动程序使用 OID \_ PM \_ 获取 \_ 协议 \_ 卸载方法 OID 来检索来自网络适配器的低功率协议卸载的参数设置。

信息缓冲区必须指向 ULONG 类型协议卸载标识符。 当 NDIS 发送之前的 [OID \_ pm \_ 将 \_ 协议 \_ 卸载](oid-pm-add-protocol-offload.md)OID 请求添加到基础网络适配器时，ndis 在 [**ndis \_ PM \_ 协议 \_ 卸载**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)结构的 **ProtocolOffloadId** 成员中设置此协议卸载标识符。

微型端口驱动程序为请求返回以下状态代码之一：

<a href="" id="ndis-status-success"></a>NDIS \_ 状态 \_ 成功  
已成功检索请求的数据。 信息缓冲区包含相应的 NDIS \_ PM \_ 协议 \_ 卸载结构。

<a href="" id="ndis-status-pending"></a>NDIS \_ 状态 \_ 挂起  
请求正在等待完成。 最终状态代码和结果将传递给调用方的 OID 请求完成处理程序。

<a href="" id="ndis-status-invalid-parameter"></a>NDIS \_ 状态 \_ 无效 \_ 参数  
指定的协议卸载标识符无效。

<a href="" id="ndis-status-buffer-too-short"></a>NDIS \_ 状态 \_ 缓冲区 \_ 太 \_ 短  
信息缓冲区太短。 NDIS 设置 **数据。查询 \_ 信息。** 将 NDIS OID 请求结构中的成员 BytesNeeded \_ \_ 为所需的最小缓冲区大小。

<a href="" id="ndis-status-not-supported"></a>\_ \_ 不支持 NDIS \_ 状态  
此微型端口驱动程序的 NDIS 版本低于6.20。

<a href="" id="ndis-status-failure"></a>NDIS \_ 状态 \_ 故障  
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
<td><p>Version</p></td>
<td><p>在 NDIS 6.20 和更高版本中受支持。 对于微型端口驱动程序是必需的。 （请参见“备注”部分。）</p></td>
</tr>
<tr class="even">
<td><p>标题</p></td>
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS \_ PM \_ 协议 \_ 卸载**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)

[OID \_ PM \_ 添加 \_ 协议 \_ 卸载](oid-pm-add-protocol-offload.md)

 

