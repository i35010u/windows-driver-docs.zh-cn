---
title: OID_SWITCH_NIC_RESTORE_COMPLETE
description: HYPER-V 可扩展交换机的协议边缘发出一个对象标识符 (OID) 组请求的 OID_SWITCH_NIC_RESTORE_COMPLETE 以通知有关要还原运行时数据的操作的完成 HYPER-V 可扩展交换机扩展。
ms.assetid: E47EBA55-FF35-4366-AF9C-A714C2E6F8FE
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SWITCH_NIC_RESTORE_COMPLETE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: cff184050292a50e18f0ab0593c1e556918a1ac8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543448"
---
# <a name="oidswitchnicrestorecomplete"></a>OID\_交换机\_NIC\_还原\_完成


HYPER-V 可扩展交换机的协议边缘发出对象标识符 (OID) 组请求的 OID\_切换\_NIC\_还原\_完成要通知的 HYPER-V 可扩展交换机扩展若要运行时数据还原操作完成。 通过此操作，该扩展将还原的端口和其关联的网络适配器连接为其运行时数据。

**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含一个指向[ **NDIS\_交换机\_NIC\_保存\_状态**](https://msdn.microsoft.com/library/windows/hardware/hh598216)结构。 可扩展交换机的协议边缘分配了此结构。

<a name="remarks"></a>备注
-------

当它收到 OID 集请求的 OID\_交换机\_NIC\_还原\_完成，该扩展必须遵守以下原则：

-   该扩展不能修改[ **NDIS\_交换机\_NIC\_保存\_状态**](https://msdn.microsoft.com/library/windows/hardware/hh598216)与 OID 请求关联的结构。
-   扩展必须调用[ **NdisFOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561830)转发此 OID 设置请求为可扩展交换机驱动程序堆栈中的基础扩展。 该扩展会 OID 请求必须失败。

OID 设置请求的 OID\_切换\_NIC\_还原\_完成最终由可扩展交换机的基础的微型端口边缘。 微型端口边缘收到此 OID 方法请求后，它完成 OID 请求使用 NDIS\_状态\_成功。 这会通知可扩展交换机的协议边缘可扩展交换机驱动程序堆栈中的所有扩展已都完成保存操作。

有关如何将保存为可扩展交换机端口的运行时数据的详细信息，请参阅[保存的 HYPER-V 可扩展切换运行时数据](https://msdn.microsoft.com/library/windows/hardware/hh598299)。

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
<td><p>版本</p></td>
<td><p>支持在 NDIS 6.30 和更高版本。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


****
[**NDIS\_OID\_REQUEST**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NDIS\_SWITCH\_NIC\_SAVE\_STATE**](https://msdn.microsoft.com/library/windows/hardware/hh598216)

 

 




