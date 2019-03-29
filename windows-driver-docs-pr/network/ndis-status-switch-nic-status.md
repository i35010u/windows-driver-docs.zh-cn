---
title: NDIS_STATUS_SWITCH_NIC_STATUS
description: NDIS_STATUS_SWITCH_NIC_STATUS 状态指示用于封装从绑定到外部网络适配器的 HYPER-V 可扩展交换机的物理网络适配器的状态指示。
ms.assetid: 51A3BE6A-35F1-4AF0-91C0-94681640BD64
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_SWITCH_NIC_STATUS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: cffe960cf89909e93c8cc1f6e8fcd81b1e2fb429
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562404"
---
# <a name="ndisstatusswitchnicstatus"></a>NDIS\_状态\_交换机\_NIC\_状态


**NDIS\_状态\_交换机\_NIC\_状态**状态指示用于封装从绑定到外部网络的物理网络适配器的状态指示HYPER-V 可扩展交换机的适配器。 通过此封装状态指示转发到可扩展交换机驱动程序堆栈。

**StatusBuffer**的成员[ **NDIS\_状态\_指示**](https://msdn.microsoft.com/library/windows/hardware/ff567373)结构，这种指示包含指向[ **NDIS\_交换机\_NIC\_状态\_指示**](https://msdn.microsoft.com/library/windows/hardware/hh598217)结构。

<a name="remarks"></a>备注
-------

当基础物理网络适配器发出 NDIS 状态指示时，它接收的外部网络适配器。 在此情况下，可扩展交换机接口执行以下步骤：

1.  该接口封装内的状态指示[ **NDIS\_交换机\_NIC\_状态\_指示**](https://msdn.microsoft.com/library/windows/hardware/hh598217)结构。

2.  界面问题**NDIS\_状态\_切换\_NIC\_状态**状态指示转发可扩展交换机驱动程序堆栈中向上的封装的状态指示。 这允许修改封装的状态指示可扩展交换机扩展。

    通常情况下，该扩展将修改封装的状态指示若要更改绑定到外部网络适配器的物理适配器的基础团队的当前卸载功能。

    有关在其中的物理网络适配器可以绑定到外部网络适配器的不同配置的详细信息，请参阅[的物理网络适配器配置的类型](https://msdn.microsoft.com/library/windows/hardware/hh582274)。

3.  当**NDIS\_状态\_切换\_NIC\_状态**状态指示接收到堆栈中的基础可扩展交换机协议驱动程序，该接口将转发解封到过量协议或筛选器驱动程序的状态指示。

扩展还可能发起到过量可扩展交换机驱动程序堆栈中的驱动程序封装的硬件卸载状态指示。 这也允许更改附加到外部网络适配器的物理适配器的基础团队的当前卸载功能的驱动程序。 团队的适配器绑定到外部网络适配器，仅在团队的常见功能会播发到 NDIS 或基础协议和筛选器驱动程序。 该扩展可以通过发起封装的状态指示要播发由团队中的某些适配器支持的功能扩展的播发的功能。

例如，扩展可以发出封装[ **NDIS\_状态\_接收\_筛选器\_当前\_功能**](ndis-status-receive-filter-current-capabilities.md)若要更改整个团队的当前已启用的接收筛选器功能的指示。

详细了解如何将转发或源自**NDIS\_状态\_交换机\_NIC\_状态**指标，请参阅[从管理 NDIS 状态指示物理网络适配器](https://msdn.microsoft.com/library/windows/hardware/hh598199)。

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
<td><p>Header</p></td>
<td>Ndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


****
[**NDIS\_状态\_指示**](https://msdn.microsoft.com/library/windows/hardware/ff567373)

[**NDIS\_状态\_接收\_筛选器\_当前\_功能**](ndis-status-receive-filter-current-capabilities.md)

 

 




