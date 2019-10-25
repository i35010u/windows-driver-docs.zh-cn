---
title: OID_SWITCH_NIC_SAVE_COMPLETE
description: Hyper-v 可扩展交换机的协议边缘发出 OID_SWITCH_NIC_SAVE_COMPLETE 的对象标识符（OID）设置请求，通知 Hyper-v 可扩展交换机扩展完成操作的完成以保存运行时数据。
ms.assetid: 75D4C0D5-B4B2-493D-8D1D-400F60613FCA
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SWITCH_NIC_SAVE_COMPLETE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 5f8a137c580e31712ff882044489b5eda4f14d96
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843947"
---
# <a name="oid_switch_nic_save_complete"></a>OID\_交换机\_NIC\_保存\_完成


Hyper-v 可扩展交换机的协议边缘发出\_SWITCH\_NIC 的对象标识符（OID）设置请求，\_保存\_完成，通知 Hyper-v 可扩展交换机扩展有关操作完成的完成情况运行时数据。 完成此操作后，扩展将为端口及其关联的网络适配器连接保存运行时数据。

[**Ndis\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**NDIS\_SWITCH\_NIC 的指针\_保存\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)结构。

<a name="remarks"></a>备注
-------

当收到 oid\_SWITCH\_NIC 的 OID 集请求时\_保存\_完成，扩展必须遵循以下准则：

-   扩展不能修改[**NDIS\_交换机\_NIC\_保存**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)与 OID 请求关联\_状态结构。

-   扩展必须调用[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest) ，以便将此 OID 集请求转发到可扩展交换机驱动程序堆栈中的基础扩展。 此扩展不能使 OID 请求失败。

Oid\_交换机\_\_\_NIC 的 oid 设置请求将最终由可扩展交换机的基础微型端口边缘处理。 在微型端口边缘收到此 OID 方法请求后，它将完成 OID 请求，并将 NDIS\_状态\_SUCCESS。 这会通知可扩展交换机的协议边缘：可扩展交换机驱动程序堆栈中的所有扩展都已完成保存操作。

有关如何为可扩展交换机端口保存运行时数据的详细信息，请参阅[保存 Hyper-v 可扩展交换机运行时数据](https://docs.microsoft.com/windows-hardware/drivers/network/saving-hyper-v-extensible-switch-run-time-data)。

### <a name="return-status-codes"></a>返回状态代码

可扩展交换机的基础微型端口边缘\_交换机\_NIC 上完成 oid 查询请求，\_保存\_完成，并返回以下状态代码之一。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>状态代码</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>NDIS_STATUS_SUCCESS</p></td>
<td><p>OID 请求已成功完成。</p></td>
</tr>
</tbody>
</table>

 

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
<td><p>在 NDIS 6.30 和更高版本中受支持。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


****
[**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_交换机\_NIC\_保存\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)

 

 




