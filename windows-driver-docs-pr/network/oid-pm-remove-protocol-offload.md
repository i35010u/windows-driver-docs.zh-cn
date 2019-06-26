---
title: OID_PM_REMOVE_PROTOCOL_OFFLOAD
description: 因为集请求、 NDIS 和协议驱动程序使用 OID_PM_REMOVE_PROTOCOL_OFFLOAD OID 来删除电源管理协议卸载网络适配器中。
ms.assetid: efca3018-28bf-4d91-b698-4b1c9e02f6e3
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_PM_REMOVE_PROTOCOL_OFFLOAD 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 1d651a63c3502e7e6d57766ffe5b5d6d21b05068
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354954"
---
# <a name="oidpmremoveprotocoloffload"></a>OID\_PM\_删除\_协议\_卸载


为 set 请求，NDIS 和协议驱动程序使用 OID\_PM\_删除\_协议\_卸载 OID，若要删除的电源管理协议从网络适配器卸载。 **InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构包含一个指向**ULONG**协议卸载标识符。

<a name="remarks"></a>备注
-------

NDIS 和协议驱动程序使用 OID\_PM\_删除\_协议\_卸载要删除协议的 OID 将卸载从基础的网络适配器。

**数据。设置\_INFORMATION.InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构必须指向**ULONG**值以前添加的协议卸载标识符。 NDIS 设置此协议卸载标识符**ProtocolOffloadId**的成员[ **NDIS\_PM\_协议\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)结构时 NDIS 发送之前[OID\_PM\_添加\_协议\_卸载](oid-pm-add-protocol-offload.md)OID 为基础的网络适配器的请求。

### <a name="remarks-for-miniport-driver-writers"></a>微型端口驱动程序编写的备注

NDIS 可确保缓冲区大小是至少**sizeof**(**ULONG**) 包含有效的协议卸载 id。 因此，微型端口驱动程序的[ *MiniportOidRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_oid_request)函数应返回 NDIS\_状态\_此请求成功。

**请注意**  微型端口驱动程序正在重置，如果其[ *MiniportOidRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_oid_request)函数应返回 NDIS\_状态\_不\_已接受。

 

### <a name="return-status-codes"></a>返回状态代码

NDIS 返回此请求的以下状态代码之一：

<a href="" id="ndis-status-success"></a>**NDIS\_状态\_成功**  
协议卸载已成功删除。

<a href="" id="ndis-status-pending"></a>**NDIS\_状态\_PENDING**  
请求正在等待完成。 NDIS 将传递的最终状态代码和结果到 OID 请求完成处理程序的调用方完成请求之后。

<a href="" id="ndis-status-invalid-length"></a>**NDIS\_状态\_无效\_长度**  
信息缓冲区因过小。 NDIS 集**数据。设置\_信息。BytesNeeded**中的成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)是必需的以字节为单位的最小缓冲区大小的结构。

<a href="" id="ndis-status-file-not-found"></a>**NDIS\_状态\_文件\_不\_找到**  
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
<td><p>支持 NDIS 6.20 及更高版本。 对于微型端口驱动程序是必需的。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS\_OID\_REQUEST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_PM\_协议\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)

[OID\_PM\_添加\_协议\_卸载](oid-pm-add-protocol-offload.md)

 

 




