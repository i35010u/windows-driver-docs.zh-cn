---
title: NDIS_STATUS_SWITCH_NIC_STATUS
description: NDIS_STATUS_SWITCH_NIC_STATUS 状态指示用于从绑定到 Hyper-v 可扩展交换机的外部网络适配器的物理网络适配器封装状态指示。
ms.assetid: 51A3BE6A-35F1-4AF0-91C0-94681640BD64
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_SWITCH_NIC_STATUS 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: dda703d0ad7d4f9ac5680291bcea09ac29f38130
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843514"
---
# <a name="ndis_status_switch_nic_status"></a>NDIS\_状态\_交换机\_NIC\_状态


**NDIS\_状态\_交换机\_NIC\_状态**状态指示用于从绑定到 hyper-v 可扩展交换机的外部网络适配器的物理网络适配器封装状态指示。 通过此封装，状态指示会向上转送可扩展交换机驱动程序堆栈。

对于此指示， [**ndis\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构的**StatusBuffer**成员包含指向[**NDIS\_交换机\_NIC\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_nic_status_indication)结构的指针。

<a name="remarks"></a>备注
-------

当底层物理网络适配器发出 NDIS 状态指示时，它将由外部网络适配器接收。 出现这种情况时，可扩展交换机接口将执行以下步骤：

1.  接口在[**NDIS\_交换机\_NIC\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_nic_status_indication)结构中封装状态指示。

2.  接口发出**NDIS\_状态\_交换机\_NIC\_状态**状态指示，以将封装的状态指示转发到可扩展交换机驱动程序堆栈。 这允许可扩展交换机扩展来修改封装的状态指示。

    通常，该扩展将修改封装的状态指示，以更改绑定到外部网络适配器的物理适配器的底层团队的当前卸载功能。

    有关可以将物理网络适配器绑定到外部网络适配器的不同配置的详细信息，请参阅[物理网络适配器配置的类型](https://docs.microsoft.com/windows-hardware/drivers/network/types-of-physical-network-adapter-configurations)。

3.  当**NDIS\_状态\_交换机\_NIC\_状态**状态指示由堆栈中的过量可扩展交换机协议驱动程序接收时，接口会将解封状态指示转发到过量协议或筛选器驱动程序。

扩展还可以在可扩展交换机驱动程序堆栈中为过量驱动程序发起封装的硬件卸载状态指示。 这还允许驱动程序更改附加到外部网络适配器的物理适配器的底层团队的当前卸载功能。 当适配器组绑定到外部网络适配器时，仅将团队的常见功能播发到 NDIS 或过量协议和筛选器驱动程序。 扩展可以通过将封装的状态指示起源到团队中某些适配器支持的播发功能来扩展播发功能。

例如，扩展可以发出封装的[**NDIS\_状态\_接收\_筛选器\_当前\_功能**](ndis-status-receive-filter-current-capabilities.md)指示为整个团队更改当前启用的接收筛选器功能。

若要详细了解如何转发或发起**NDIS\_状态\_交换机\_NIC\_状态**指示，请参阅[从物理网络适配器管理 ndis 状态指示](https://docs.microsoft.com/windows-hardware/drivers/network/managing-ndis-status-indications-from-physical-network-adapters)。

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
<td>Ndis .h （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


****
[**NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

[ **\_接收\_筛选器\_当前\_功能，NDIS\_状态**](ndis-status-receive-filter-current-capabilities.md)

 

 




