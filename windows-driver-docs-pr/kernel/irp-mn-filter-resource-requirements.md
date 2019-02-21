---
title: IRP_MN_FILTER_RESOURCE_REQUIREMENTS
description: PnP 管理器将此 IRP 发送到设备堆栈，因此如果适当，功能驱动程序可以调整该设备，所需的资源。功能驱动程序通常会处理此 IRP。
ms.date: 08/12/2017
ms.assetid: f43dc60e-de88-4af0-ad83-3ce3a414d880
keywords:
- IRP_MN_FILTER_RESOURCE_REQUIREMENTS 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: 253b31f8aa8033c0318f2104d6812e2619eb8396
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546826"
---
# <a name="irpmnfilterresourcerequirements"></a>IRP\_MN\_FILTER\_RESOURCE\_REQUIREMENTS


PnP 管理器将此 IRP 发送到设备堆栈，因此如果适当，功能驱动程序可以调整该设备，所需的资源。

功能驱动程序通常会处理此 IRP。

父总线驱动程序 （和总线筛选器驱动程序） 不应处理子 PDO; 此请求相反，此类驱动程序应报告在响应中的资源要求[ **IRP\_MN\_查询\_资源\_要求**](irp-mn-query-resource-requirements.md)请求。

上限和较低的筛选器驱动程序不处理此 IRP。

<a name="major-code"></a>主代码
----------

[**IRP\_MJ\_PNP**](irp-mj-pnp.md) When Sent
---------

PnP 管理器将发送此 IRP 时它正在准备，以便分配到设备的资源。

PnP 管理器将此 IRP 发送在 IRQL 被动\_级别的任意线程上下文中。

## <a name="input-parameters"></a>输入参数


**Irp-&gt;IoStatus.Information**指向[ **IO\_资源\_要求\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff550609)包含硬件设备的资源要求。 在指针位于**NULL**如果设备不使用的任何硬件资源。

**Parameters.FilterResourceRequirements.IoResourceRequirementList**还指向**IO\_资源\_要求\_列表**，但功能驱动程序应使用列表中**IoStatus**块。

## <a name="output-parameters"></a>输出参数


返回在 I/O 状态块中。

## <a name="io-status-block"></a>I/O 状态块


如果功能驱动程序处理此 IRP，它处理它在 IRP 的方式备份在堆栈上。 如果功能驱动程序已成功处理 IRP，它会设置**Irp-&gt;IoStatus.Status**于状态\_成功和集**Irp-&gt;IoStatus.Information**到指向[ **IO\_资源\_要求\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff550609)包含筛选的资源要求。 请参阅下面有关设置筛选的资源列表的详细信息"操作"部分。 如果功能驱动程序处理此 IRP 时遇到错误，它会设置错误**Irp-&gt;IoStatus.Status**。 如果功能驱动程序不处理此 IRP，它将使用[ **IoSkipCurrentIrpStackLocation** ](https://msdn.microsoft.com/library/windows/hardware/ff550355)将传递在堆栈的下层 IRP 保持不变。

上限和较低的筛选器驱动程序不处理此 IRP。 此类驱动程序调用**IoSkipCurrentIrpStackLocation**，将传递到下一步的驱动程序 IRP，不能修改**Irp-&gt;IoStatus**，并且必须完成 IRP。

父总线驱动程序不处理此 IRP。 离开**Irp-&gt;IoStatus**完成 IRP 和时。

<a name="operation"></a>操作
---------

PnP 管理器将发送[ **IRP\_MN\_查询\_资源\_要求**](irp-mn-query-resource-requirements.md)之前对该设备，该父总线驱动程序的请求功能驱动程序已附加到设备堆栈其设备对象。 若要使功能驱动程序有机会修改设备的资源要求，如果适用，即插即用管理器更高版本将发送**IRP\_MN\_筛选器\_资源\_要求**完整的设备堆栈的请求。 PnP 管理器将发送此 IRP 之前在初始设备配置过程中分配到设备的硬件资源。 PnP 管理器还可以在资源重新平衡过程中发送此 IRP。

当 PnP 管理器将发送此 IRP 时，它提供的资源要求列表，该驱动程序可以修改并返回驱动程序堆栈。 PnP 管理器会提供一个以下类型的资源要求列表 （按优先顺序列出）：

-   （从资源列表资源要求列表修改） 的强制性的配置

-   替代配置

-   基本配置

-   启动配置 （从资源列表资源要求列表修改）

如果功能驱动程序处理此 IRP，它必须设置完成例程，并处理重新启动设备堆栈手 IRP。 请参阅[插](https://msdn.microsoft.com/library/windows/hardware/ff547125)处理备份设备堆栈手 PnP IRP 的相关信息。

如果功能驱动程序未更改指向的当前列表的大小**Irp-&gt;IoStatus.Information**，驱动程序可以修改在位置列表。 如果驱动程序所需更改要求列表的大小，该驱动程序必须分配一个新[ **IO\_资源\_要求\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff550609)列表从分页内存和免费的前面的列表。 当不再需要时，即插即用管理器释放返回的结构。

功能驱动程序必须保留指向列表中的资源的顺序**Irp-&gt;IoStatus.Information**和不得更改不会处理的资源标记。 该驱动程序必须小心以调整设备的父总线支持一种方法中的要求列表。 如果功能驱动程序将新的资源添加到要求列表，并且该资源分配给设备，功能驱动程序应筛选出的该资源[ **IRP\_MN\_启动\_设备**](irp-mn-start-device.md)然后再将传递开始 IRP 向总线驱动程序。

如果设备功能驱动程序不处理此 IRP，PnP 管理器将使用指定的响应中的父总线驱动程序的资源要求[ **IRP\_MN\_查询\_资源\_要求**](irp-mn-query-resource-requirements.md)请求。

功能驱动程序必须准备好处理此 IRP 的设备驱动程序的后随时[ *AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)例程名为的设备。

请参阅[插](https://msdn.microsoft.com/library/windows/hardware/ff547125)处理的常规规则[即插即用次要 Irp](plug-and-play-minor-irps.md)。

**发送此 IRP**

保留供系统使用。 驱动程序必须发送此 IRP。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>标头</p></td>
<td>Wdm.h 中 （包括 wdm.h 中、 Ntddk.h 或 Ntifs.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**ExAllocatePoolWithTag**](https://msdn.microsoft.com/library/windows/hardware/ff544520)

[**ExFreePool**](https://msdn.microsoft.com/library/windows/hardware/ff544590)

[**IO\_资源\_要求\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff550609)

[**IRP\_MN\_START\_DEVICE**](irp-mn-start-device.md)

 

 




