---
title: OID_SWITCH_NIC_RESTORE
description: 对象标识符 (OID) 设置的 OID_SWITCH_NIC_RESTORE 的请求，以通知有关运行时数据的可还原的可扩展交换机端口和其网络适配器的可扩展交换机扩展的 HYPER-V 可扩展交换机问题的协议边缘连接。
ms.assetid: 252FB1D2-932F-4FB8-83D6-2690171D746D
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SWITCH_NIC_RESTORE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: c199635a6daf6c8130e599c37bd2de301f119b9e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555043"
---
# <a name="oidswitchnicrestore"></a>OID\_交换机\_NIC\_还原


HYPER-V 可扩展交换机的协议边缘发出对象标识符 (OID) 组请求的 OID\_切换\_NIC\_还原，以通知有关可用于还原的运行时数据的可扩展交换机扩展可扩展交换机端口，其网络适配器连接。

**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含一个指向[ **NDIS\_交换机\_NIC\_保存\_状态**](https://msdn.microsoft.com/library/windows/hardware/hh598216)结构。 可扩展交换机的协议边缘分配了此结构。

<a name="remarks"></a>备注
-------

当它收到 OID 集请求的 OID\_切换\_NIC\_还原、 可扩展的交换机扩展必须首先确定它是否拥有的运行时数据。 通过将的值进行比较来扩展实现这**ExtensionId**的成员[ **NDIS\_开关\_NIC\_保存\_状态**](https://msdn.microsoft.com/library/windows/hardware/hh598216)结构与该扩展使用自己的 GUID 值。

如果该扩展拥有可扩展交换机端口的运行时数据，它可按以下方式恢复此数据：

1.  扩展可将复制中的运行时数据**SaveData**成员添加到扩展分配存储。

    **请注意**  的值**PortId**的成员[ **NDIS\_交换机\_NIC\_保存\_状态**](https://msdn.microsoft.com/library/windows/hardware/hh598216)结构可能不同于**PortId**处运行时数据已保存的时间值。 如果运行时数据从一个主机到另一个保存在实时迁移期间，这可能发生。 但是，在实时迁移期间保留可扩展交换机端口的配置。 这样，要将运行时数据还原到可扩展交换机端口，通过使用新的扩展插件**PortId**值。

     

2.  扩展完成 OID 集请求使用 NDIS\_状态\_成功。

如果扩展不拥有指定的运行时数据，则扩展将调用[ **NdisFOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561830)转发此 OID 设置请求为可扩展交换机驱动程序堆栈中的基础扩展。 在这种情况下，该扩展不能修改[ **NDIS\_交换机\_NIC\_保存\_状态**](https://msdn.microsoft.com/library/windows/hardware/hh598216)与 OID 请求关联的结构。

如果 OID\_切换\_NIC\_可扩展交换机的微型端口边缘收到还原集请求时，它完成 OID 请求使用 NDIS\_状态\_成功。 这会通知可扩展交换机的协议边缘没有扩展名拥有的运行时数据。

有关如何还原运行时数据的详细信息，请参阅[还原的 HYPER-V 可扩展交换机运行时数据](https://msdn.microsoft.com/library/windows/hardware/hh598298)。

**请注意**  如果该扩展将通 OID 集请求，可扩展切换会失败，整个还原操作。 因此，扩展应避免它是否可以故障 OID 请求。 例如，如果扩展无法分配恢复运行时数据所必需的资源，它应失败 OID 请求，如果它不能正常工作而不还原的运行时数据。 但是，如果该扩展可以从此故障条件，它应无法 OID 集请求。

 

### <a name="return-status-codes"></a>返回状态代码

如果该扩展完成 OID 集请求的 OID\_交换机\_NIC\_还原，它返回以下状态代码的一个实例。

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
<tr class="even">
<td><p>NDIS_STATUS_<em>Xxx</em></p></td>
<td><p>请求由于其他原因而失败。</p></td>
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

[**NdisFOidRequest**](https://msdn.microsoft.com/library/windows/hardware/ff561830)

 

 




