---
title: OID_PM_REMOVE_PROTOCOL_OFFLOAD
description: 作为一个集请求，NDIS 和协议驱动程序使用 OID_PM_REMOVE_PROTOCOL_OFFLOAD OID 从网络适配器中删除电源管理协议卸载。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_PM_REMOVE_PROTOCOL_OFFLOAD 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 7aa4e9854edbbf1c30dbfde3f5555bf015e7d4c6
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102249018"
---
# <a name="oid_pm_remove_protocol_offload"></a>OID \_ PM \_ 删除 \_ 协议 \_ 卸载


作为一个集请求，NDIS 和协议驱动程序使用 OID \_ PM \_ 删除 \_ 协议 \_ 卸载 OID 从网络适配器中删除电源管理协议卸载。 [**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)结构的 **InformationBuffer** 成员包含指向 **ULONG** 协议卸载标识符的指针。

<a name="remarks"></a>备注
-------

NDIS 和协议驱动程序使用 OID \_ PM \_ 删除 \_ 协议 \_ 卸载 OID 从基础网络适配器中删除协议卸载。

**数据。设置 \_ 信息。** 对于之前添加的协议卸载标识符， [**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)结构的 InformationBuffer 成员必须指向 **ULONG** 值。 当 NDIS 发送了前面的 [OID \_ pm \_ 将 \_ 协议 \_ 卸载](oid-pm-add-protocol-offload.md)OID 请求发送到基础网络适配器时，ndis 在 [**ndis \_ PM \_ 协议 \_ 卸载**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)结构的 **ProtocolOffloadId** 成员中设置此协议卸载标识符。

### <a name="remarks-for-miniport-driver-writers"></a>微型端口驱动程序编写器的备注

NDIS 确保缓冲区大小至少为 **sizeof** (**ULONG**) 并包含有效的协议卸载 ID。 因此，微型端口驱动程序的 [*MiniportOidRequest*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request) 函数应返回 \_ \_ 此请求的 NDIS 状态成功。

**注意**  如果重置微型端口驱动程序，其 [*MiniportOidRequest*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request) 函数应返回 NDIS \_ 状态 " \_ 不接受" \_ 。

 

### <a name="return-status-codes"></a>返回状态代码

NDIS 为此请求返回以下状态代码之一：

<a href="" id="ndis-status-success"></a>**NDIS \_ 状态 \_ 成功**  
已成功删除协议卸载。

<a href="" id="ndis-status-pending"></a>**NDIS \_ 状态 \_ 挂起**  
请求正在等待完成。 请求完成后，NDIS 会将最终状态代码和结果传递给调用方的 OID 请求完成处理程序。

<a href="" id="ndis-status-invalid-length"></a>**NDIS \_ 状态 \_ 无效 \_ 长度**  
信息缓冲区太小。 NDIS 设置 **数据。设置 \_ 信息。** 将 [**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request) 结构中的成员 BytesNeeded 为所需的最小缓冲区大小（以字节为单位）。

<a href="" id="ndis-status-file-not-found"></a>**\_ \_ \_ \_ 找不到 NDIS 状态文件**  
OID 请求中的协议卸载标识符无效。

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
<td><p>在 NDIS 6.20 和更高版本中受支持。 对于微型端口驱动程序是必需的。</p></td>
</tr>
<tr class="even">
<td><p>标题</p></td>
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)

[**NDIS \_ PM \_ 协议 \_ 卸载**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)

[OID \_ PM \_ 添加 \_ 协议 \_ 卸载](oid-pm-add-protocol-offload.md)

 

