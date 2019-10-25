---
title: OID_PM_REMOVE_PROTOCOL_OFFLOAD
description: 作为一个集请求，NDIS 和协议驱动程序使用 OID_PM_REMOVE_PROTOCOL_OFFLOAD OID 从网络适配器中删除电源管理协议卸载。
ms.assetid: efca3018-28bf-4d91-b698-4b1c9e02f6e3
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_PM_REMOVE_PROTOCOL_OFFLOAD 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 1e3d78133e8d79eb2b42824a3cade7658545068f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844050"
---
# <a name="oid_pm_remove_protocol_offload"></a>OID\_PM\_删除\_协议\_卸载


作为一个集请求，NDIS 和协议驱动程序使用 OID\_PM\_删除\_协议\_卸载 OID，以从网络适配器中删除电源管理协议卸载。 [ **\_OID 的 NDIS\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向**ULONG**协议卸载标识符的指针。

<a name="remarks"></a>备注
-------

NDIS 和协议驱动程序使用 OID\_PM\_删除\_协议\_卸载 OID，以从基础网络适配器中删除协议卸载。

**数据。设置\_信息。** [**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的 InformationBuffer 成员必须指向以前添加的协议卸载标识符的**ULONG**值。 当 NDIS 发送以前的 OID\_PM\_添加\_协议时，NDIS 在 Ndis\_PM 的**ProtocolOffloadId**成员中设置此协议卸载标识符[ **\_协议\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)结构[\_](oid-pm-add-protocol-offload.md)将 OID 请求卸载到基础网络适配器。

### <a name="remarks-for-miniport-driver-writers"></a>微型端口驱动程序编写器的备注

NDIS 确保缓冲区大小至少为**sizeof**（**ULONG**）并且包含有效的协议卸载 ID。 因此，微型端口驱动程序的[*MiniportOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)函数应返回此请求\_成功的 NDIS\_状态。

**请注意**  如果重新设置微型端口驱动程序，其[*MiniportOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)函数应返回 NDIS\_状态\_不\_接受。

 

### <a name="return-status-codes"></a>返回状态代码

NDIS 为此请求返回以下状态代码之一：

<a href="" id="ndis-status-success"></a>**成功的 NDIS\_状态\_**  
已成功删除协议卸载。

<a href="" id="ndis-status-pending"></a>**NDIS\_状态\_挂起**  
请求正在等待完成。 请求完成后，NDIS 会将最终状态代码和结果传递给调用方的 OID 请求完成处理程序。

<a href="" id="ndis-status-invalid-length"></a>**NDIS\_状态\_无效的\_长度**  
信息缓冲区太小。 NDIS 设置**数据。设置\_信息。** \_OID 中的 BytesNeeded 成员[ **\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构到所需的最小缓冲区大小（以字节为单位）。

<a href="" id="ndis-status-file-not-found"></a>**找\_不到\_文件\_\_的 NDIS 状态**  
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
<td><p>版本</p></td>
<td><p>在 NDIS 6.20 和更高版本中受支持。 对于微型端口驱动程序是必需的。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_PM\_协议\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)

[OID\_PM\_添加\_协议\_卸载](oid-pm-add-protocol-offload.md)

 

 




