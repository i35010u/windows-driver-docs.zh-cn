---
title: OID_SWITCH_NIC_SAVE_COMPLETE
description: Hyper-v 可扩展交换机的协议边缘 (OID 发出对象标识符) 设置 OID_SWITCH_NIC_SAVE_COMPLETE 请求，通知 Hyper-v 可扩展交换机扩展完成操作的完成以保存运行时数据。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SWITCH_NIC_SAVE_COMPLETE 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: f624a6342d5108894ca581b2446bfcbcecb9bc3b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837923"
---
# <a name="oid_switch_nic_save_complete"></a>OID \_ 交换机 \_ NIC \_ 保存 \_ 完毕


Hyper-v 可扩展交换机的协议边缘 (OID 发出对象标识符) 设置 OID \_ 交换机 \_ NIC \_ SAVE \_ 完成，通知 hyper-v 可扩展交换机扩展关于操作的完成以保存运行时数据。 完成此操作后，扩展将为端口及其关联的网络适配器连接保存运行时数据。

[**Ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的 **InformationBuffer** 成员包含指向 [**ndis \_ 交换机 \_ NIC \_ 保存 \_ 状态**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)结构的指针。

<a name="remarks"></a>备注
-------

当它收到 oid 交换机 NIC SAVE 完成的 OID 设置请求时 \_ \_ \_ \_ ，扩展必须遵循以下准则：

-   扩展不得修改与 OID 请求关联的 [**NDIS \_ 交换机 \_ NIC \_ 保存 \_ 状态**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state) 结构。

-   扩展必须调用 [**NdisFOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest) ，以便将此 OID 集请求转发到可扩展交换机驱动程序堆栈中的基础扩展。 此扩展不能使 OID 请求失败。

Oid \_ 交换机 \_ NIC 保存完成的 oid \_ 设置 \_ 最终由可扩展交换机的基础微型端口边缘处理。 在微型端口边缘收到此 OID 方法请求后，它将完成具有 NDIS 状态成功的 OID \_ 请求 \_ 。 这会通知可扩展交换机的协议边缘：可扩展交换机驱动程序堆栈中的所有扩展都已完成保存操作。

有关如何为可扩展交换机端口保存运行时数据的详细信息，请参阅 [保存 Hyper-v 可扩展交换机 Run-Time 数据](./managing-hyper-v-extensible-switch-run-time-data.md)。

### <a name="return-status-codes"></a>返回状态代码

可扩展交换机的基础微型端口边缘完成 OID \_ 交换机 NIC SAVE 完成的 oid 查询 \_ 请求 \_ \_ ，并返回以下状态代码之一。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>状态代码</th>
<th>说明</th>
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
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


****
[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS \_ 交换机 \_ NIC \_ 保存 \_ 状态**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)

 

