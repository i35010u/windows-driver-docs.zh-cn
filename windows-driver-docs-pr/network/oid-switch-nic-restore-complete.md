---
title: OID_SWITCH_NIC_RESTORE_COMPLETE
description: HYPER-V 可扩展交换机的协议边缘发出一个对象标识符 (OID) 组请求的 OID_SWITCH_NIC_RESTORE_COMPLETE 以通知有关要还原运行时数据的操作的完成 HYPER-V 可扩展交换机扩展。
ms.assetid: E47EBA55-FF35-4366-AF9C-A714C2E6F8FE
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SWITCH_NIC_RESTORE_COMPLETE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 12035e6a5a929b1caa6b08fb24d8ee461822f507
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385840"
---
# <a name="oidswitchnicrestorecomplete"></a>OID\_交换机\_NIC\_还原\_完成


HYPER-V 可扩展交换机的协议边缘发出对象标识符 (OID) 组请求的 OID\_切换\_NIC\_还原\_完成要通知的 HYPER-V 可扩展交换机扩展若要运行时数据还原操作完成。 通过此操作，该扩展将还原的端口和其关联的网络适配器连接为其运行时数据。

**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构包含一个指向[ **NDIS\_交换机\_NIC\_保存\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)结构。 可扩展交换机的协议边缘分配了此结构。

<a name="remarks"></a>备注
-------

当它收到 OID 集请求的 OID\_交换机\_NIC\_还原\_完成，该扩展必须遵守以下原则：

-   该扩展不能修改[ **NDIS\_交换机\_NIC\_保存\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)与 OID 请求关联的结构。
-   扩展必须调用[ **NdisFOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfoidrequest)转发此 OID 设置请求为可扩展交换机驱动程序堆栈中的基础扩展。 该扩展会 OID 请求必须失败。

OID 设置请求的 OID\_切换\_NIC\_还原\_完成最终由可扩展交换机的基础的微型端口边缘。 微型端口边缘收到此 OID 方法请求后，它完成 OID 请求使用 NDIS\_状态\_成功。 这会通知可扩展交换机的协议边缘可扩展交换机驱动程序堆栈中的所有扩展已都完成保存操作。

有关如何将保存为可扩展交换机端口的运行时数据的详细信息，请参阅[保存的 HYPER-V 可扩展切换运行时数据](https://docs.microsoft.com/windows-hardware/drivers/network/saving-hyper-v-extensible-switch-run-time-data)。

### <a name="return-status-codes"></a>返回状态代码

如果该扩展完成的 OID 集请求[OID\_交换机\_NIC\_还原\_完成](oid-switch-nic-restore.md)，它将返回一个下面的状态代码。

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
<td><p>Version</p></td>
<td><p>支持在 NDIS 6.30 和更高版本。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


****
[**NDIS\_OID\_REQUEST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_SWITCH\_NIC\_SAVE\_STATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)

 

 




