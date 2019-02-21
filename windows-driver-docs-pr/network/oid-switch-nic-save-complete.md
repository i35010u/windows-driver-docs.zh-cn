---
title: OID_SWITCH_NIC_SAVE_COMPLETE
description: HYPER-V 可扩展交换机的协议边缘发出一个对象标识符 (OID) 组请求的 OID_SWITCH_NIC_SAVE_COMPLETE 以通知有关保存运行时数据操作完成的 HYPER-V 可扩展交换机扩展。
ms.assetid: 75D4C0D5-B4B2-493D-8D1D-400F60613FCA
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SWITCH_NIC_SAVE_COMPLETE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: f13707aebec432109302c8293574e7b94aaa21ae
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544003"
---
# <a name="oidswitchnicsavecomplete"></a>OID\_交换机\_NIC\_保存\_完成


HYPER-V 可扩展交换机的协议边缘发出对象标识符 (OID) 组请求的 OID\_切换\_NIC\_保存\_完成通知关于完成的 HYPER-V 可扩展交换机扩展要保存运行时数据的操作。 通过此操作，该扩展将保存的端口和其关联的网络适配器连接的运行时数据。

**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含一个指向[ **NDIS\_交换机\_NIC\_保存\_状态**](https://msdn.microsoft.com/library/windows/hardware/hh598216)结构。

<a name="remarks"></a>备注
-------

当它收到 OID 集请求的 OID\_交换机\_NIC\_保存\_完成，该扩展必须遵守以下原则：

-   该扩展不能修改[ **NDIS\_交换机\_NIC\_保存\_状态**](https://msdn.microsoft.com/library/windows/hardware/hh598216)与 OID 请求关联的结构。

-   扩展必须调用[ **NdisFOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561830)转发此 OID 设置请求为可扩展交换机驱动程序堆栈中的基础扩展。 该扩展会 OID 请求必须失败。

OID 设置请求的 OID\_切换\_NIC\_保存\_完成最终由可扩展交换机的基础的微型端口边缘。 微型端口边缘收到此 OID 方法请求后，它完成 OID 请求使用 NDIS\_状态\_成功。 这会通知可扩展交换机的协议边缘可扩展交换机驱动程序堆栈中的所有扩展已都完成保存操作。

有关如何将保存为可扩展交换机端口的运行时数据的详细信息，请参阅[保存的 HYPER-V 可扩展切换运行时数据](https://msdn.microsoft.com/library/windows/hardware/hh598299)。

### <a name="return-status-codes"></a>返回状态代码

可扩展交换机的基础的微型端口边缘完成 OID 查询请求的 OID\_切换\_NIC\_保存\_完成并返回一个的以下状态代码。

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

 

 




