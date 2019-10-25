---
title: IRP_MN_FILTER_RESOURCE_REQUIREMENTS
description: PnP 管理器将此 IRP 发送到设备堆栈，以便函数驱动程序可以根据需要调整设备所需的资源。函数驱动程序通常处理此 IRP。
ms.date: 08/12/2017
ms.assetid: f43dc60e-de88-4af0-ad83-3ce3a414d880
keywords:
- IRP_MN_FILTER_RESOURCE_REQUIREMENTS 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: d1ad420323974af261444fcfc3d53b7a62136656
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838580"
---
# <a name="irp_mn_filter_resource_requirements"></a>IRP\_MN\_筛选器\_资源\_要求


PnP 管理器将此 IRP 发送到设备堆栈，以便函数驱动程序可以根据需要调整设备所需的资源。

函数驱动程序通常处理此 IRP。

父总线驱动程序（和总线筛选器驱动程序）不应处理子 PDO 的此请求;相反，此类驱动程序应报告资源要求，以响应[**IRP\_MN\_查询\_资源\_要求**](irp-mn-query-resource-requirements.md)请求。

上限和小写筛选器驱动程序不处理此 IRP。

<a name="major-code"></a>主代码
----------

[**IRP\_MJ\_PNP**](irp-mj-pnp.md)发送时间
---------

PnP 管理器将在准备向设备分配资源时发送此 IRP。

PnP 管理器在任意线程的上下文中以 IRQL 被动\_级别发送此 IRP。

## <a name="input-parameters"></a>输入参数


**Irp-&gt;IoStatus**指向[**IO\_资源\_要求\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_resource_requirements_list)包含设备硬件资源要求的列表。 如果设备不消耗硬件资源，则指针为**NULL** 。

**FilterResourceRequirements. IoResourceRequirementList**还 **\_列表指向 IO\_资源\_需求**，但函数驱动程序应使用**IoStatus**块中的列表。

## <a name="output-parameters"></a>输出参数


在 i/o 状态块中返回。

## <a name="io-status-block"></a>I/O 状态块


如果函数驱动程序处理此 IRP，则它会按照 IRP 的方式备份堆栈。 如果函数驱动程序成功处理 IRP，则它会将**irp&gt;IoStatus**设置为 STATUS\_SUCCESS，并将**irp&gt;IoStatus**设置为指向[**IO\_资源\_要求的指针 @no__t**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_resource_requirements_list)包含筛选的资源要求的 _9_ 列表。 有关设置筛选的资源列表的详细信息，请参阅下面的 "操作" 部分。 如果函数驱动程序在处理此 IRP 时遇到错误，则会在**irp&gt;IoStatus**中设置错误。 如果函数驱动程序不处理此 IRP，它将使用[**IoSkipCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)将 irp 向下传递到不变的堆栈。

上限和小写筛选器驱动程序不处理此 IRP。 此类驱动程序调用**IoSkipCurrentIrpStackLocation**，将 irp 向下传递到下一个驱动程序，不能修改**irp&gt;IoStatus**，且不能完成 irp。

父总线驱动程序无法处理此 IRP。 它会将**irp&gt;IoStatus**保持原样，并完成 irp。

<a name="operation"></a>操作
---------

PnP 管理器将[**IRP\_MN\_查询\_资源\_要求**](irp-mn-query-resource-requirements.md)请求发送到设备的父总线驱动程序，然后将其设备对象附加到设备堆栈。 为了使函数驱动程序有机会修改设备的资源要求（如果适用），PnP 管理器稍后会将**IRP\_MN\_筛选器**发送到完整设备堆栈\_资源\_要求请求。 PnP 管理器将在初始设备配置过程中向设备分配硬件资源之前发送此 IRP。 PnP 管理器还可能在重新平衡资源期间发送此 IRP。

当 PnP 管理器发送此 IRP 时，它将为驱动程序堆栈提供资源需求列表，驱动程序可以修改并返回该列表。 PnP 管理器提供以下类型的资源要求列表（按优先级顺序列出）：

-   强制配置（从资源列表修改为资源需求列表）

-   替代配置

-   基本配置

-   启动配置（从资源列表修改为资源需求列表）

如果函数驱动程序处理此 IRP，则它必须设置完成例程，并按其备份设备堆栈的方式处理 IRP。 请参阅[即插即用](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)，了解有关如何处理 PnP IRP 的详细信息，请参阅备份设备堆栈。

如果函数驱动程序未更改 Irp 所指向的当前列表的大小 **&gt;IoStatus**，则驱动程序可以就地修改列表。 如果驱动程序需要更改需求列表的大小，则驱动程序必须分配新的[**IO\_资源\_需求\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_resource_requirements_list)从分页内存中列表，并释放以前的列表。 当不再需要返回的结构时，PnP 管理器会将其释放。

函数驱动程序必须保留由**Irp&gt;** 的列表中资源的顺序，而不能更改它不处理的资源标记。 驱动程序必须小心调整设备的父总线支持的方法列表。 如果函数驱动程序向需求列表中添加了新资源，并且该资源已分配给设备，则函数驱动程序应在将启动 IRP 向下传递到之前从[**irp\_MN\_启动\_设备**](irp-mn-start-device.md)总线驱动程序。

如果设备的函数驱动程序未处理此 IRP，则 PnP 管理器将使用父总线驱动程序指定的资源要求来响应[**IRP\_MN\_查询\_资源\_要求**](irp-mn-query-resource-requirements.md)请求。

在为设备调用了驱动程序的[*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)例程之后，必须准备好函数驱动程序为设备处理此 IRP。

请参阅[即插即用](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)，了解用于处理[即插即用次要 irp](plug-and-play-minor-irps.md)的一般规则。

**正在发送此 IRP**

保留供系统使用。 驱动程序不得发送此 IRP。

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
<td>Wdm .h （包括 Wdm、Ntddk 或 Ntifs）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**ExAllocatePoolWithTag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)

[**ExFreePool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool)

[**IO\_资源\_需求\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_resource_requirements_list)

[**IRP\_MN\_启动\_设备**](irp-mn-start-device.md)

 

 




