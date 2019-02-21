---
title: IRP_MN_QUERY_RESOURCE_REQUIREMENTS
description: PnP 管理器使用此 IRP 获取设备的资源要求列表。总线驱动程序必须处理此请求适用于需要的硬件资源及其子设备。
ms.date: 08/12/2017
ms.assetid: 5a77f8d6-2b6b-4eff-8d48-e7942976ec52
keywords:
- IRP_MN_QUERY_RESOURCE_REQUIREMENTS 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: 905339d2b240448ba692195903933eac781fed71
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525793"
---
# <a name="irpmnqueryresourcerequirements"></a>IRP\_MN\_查询\_资源\_要求


PnP 管理器使用此 IRP 获取设备的资源要求列表。

总线驱动程序必须处理此请求适用于需要的硬件资源及其子设备。 总线筛选器驱动程序可以处理此请求。 函数和筛选器驱动程序不处理此 IRP。

<a name="major-code"></a>主代码
----------

[**IRP\_MJ\_PNP**](irp-mj-pnp.md) When Sent
---------

PnP 管理器将发送此 IRP，枚举设备时之前资源分配到一台设备，, 以及时驱动程序报告其设备的资源要求已更改。

PnP 管理器将此 IRP 发送在 IRQL 被动\_级别在任意线程上下文中。

## <a name="input-parameters"></a>输入参数


无

## <a name="output-parameters"></a>输出参数


返回在 I/O 状态块中。

## <a name="io-status-block"></a>I/O 状态块


处理此 IRP 的驱动程序设置**Irp-&gt;IoStatus.Status**于状态\_成功或相应的错误状态。

如果成功，驱动程序设置**Irp-&gt;IoStatus.Information**指向的指针到[ **IO\_资源\_要求\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff550609)包含所需的信息。 发生错误时，驱动程序设置**Irp-&gt;IoStatus.Information**为零。

<a name="operation"></a>操作
---------

如果总线驱动程序返回到此 IRP 的响应中的资源要求列表，它会分配**IO\_资源\_要求\_列表**从分页的内存。 当不再需要时，即插即用管理器释放缓冲区。

如果设备不需要任何硬件资源，将设备的总线驱动程序会完成 IRP ([**IoCompleteRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548343)) 而无需修改**Irp-&gt;IoStatus.Status**或**Irp-&gt;IoStatus.Information**。

如果总线筛选器驱动程序处理此 IRP，它会修改总线驱动程序创建的资源要求列表。 总线筛选器驱动程序修改 IRP 的方式重新启动设备堆栈上的列表。 总线筛选器驱动程序必须保留的资源要求列表中的资源的顺序和不得更改不会处理的资源标记。 如果总线筛选器驱动程序发生更改的资源要求列表的大小，该驱动程序必须从分页内存分配新的结构并释放以前的结构。 如果总线筛选器驱动程序向列表添加新的资源要求和资源分配给设备，该驱动程序必须筛选出的新资源[ **IRP\_MN\_启动\_设备**](irp-mn-start-device.md) IRP，因此它不传递到总线驱动程序。

函数和非总线筛选器驱动程序不处理此 IRP;它们将其传递给下一个较低驱动程序和无变化**Irp-&gt;IoStatus**。

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


[**IO\_资源\_要求\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff550609)

 

 




