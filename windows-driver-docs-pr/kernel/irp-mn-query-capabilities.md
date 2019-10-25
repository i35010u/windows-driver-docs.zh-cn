---
title: IRP_MN_QUERY_CAPABILITIES
description: PnP 管理器发送此 IRP 以获取设备的功能，例如设备是否可以锁定或弹出。函数和筛选器驱动程序在更改总线驱动程序支持的功能时，可以处理此请求。
ms.date: 08/12/2017
ms.assetid: 3c968a46-5bfb-4579-b09a-ad6bce4d9e3b
keywords:
- IRP_MN_QUERY_CAPABILITIES 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: 22ec1317e0f647511c79298a2948a8ea0a78eac4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838576"
---
# <a name="irp_mn_query_capabilities"></a>IRP\_MN\_查询\_功能


PnP 管理器发送此 IRP 以获取设备的功能，例如设备是否可以锁定或弹出。

函数和筛选器驱动程序在更改总线驱动程序支持的功能时，可以处理此请求。 总线驱动程序必须为其子设备处理此请求。

<a name="major-code"></a>主代码
----------

[**IRP\_MJ\_PNP**](irp-mj-pnp.md)发送时间
---------

在枚举设备后，PnP 管理器会立即将 IRP 发送到设备的总线驱动程序。 PnP 管理器会在设备的所有驱动程序都已启动设备后再次发送此 IRP。 驱动程序可以发送此 IRP 来获取设备功能。

PnP 管理器和驱动程序以 IRQL 被动\_级别将此 IRP 发送到任意线程上下文中。

## <a name="input-parameters"></a>输入参数


[**IO\_堆栈\_位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)结构的**DeviceCapabilities**成员指向一个[**设备\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)结构，该结构包含有关设备功能的信息。

## <a name="output-parameters"></a>输出参数


**DeviceCapabilities**指向**设备\_功能**结构，反映处理 IRP 的驱动程序所做的任何修改。

## <a name="io-status-block"></a>I/O 状态块


驱动程序将**Irp&gt;IoStatus**设置为状态\_成功，或设置为适当的错误状态，如状态\_不成功。

如果函数或筛选器驱动程序不处理此 IRP，它将调用[**IoSkipCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)并将 IRP 向下传递到下一个驱动程序。 此类驱动程序不得修改**irp&gt;IoStatus** ，并且不得完成 Irp。

总线驱动程序将**irp&gt;** 设置为 IoStatus，并完成 irp。

<a name="operation"></a>操作
---------

枚举设备后，在为设备加载函数和筛选器驱动程序之前，PnP 管理器会将**IRP\_MN\_查询\_功能**请求发送到设备的父总线驱动程序。 总线驱动程序必须在[**设备\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)结构中设置任何相关值，并将其返回到 PnP 管理器。

构建设备堆栈并且驱动程序启动了设备后，PnP 管理器将再次发送此 IRP，以首先由设备堆栈顶部的驱动程序处理，然后再发送到堆栈中的每个较低的驱动程序。 函数和筛选器驱动程序可以设置[*IoCompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)例程，并按照备份设备堆栈的方式处理此 IRP。

驱动程序应在将 IRP 传递到下一个较低版本的驱动程序之前添加功能。

使用 IRP 完成所有较低版本的驱动程序后，驱动程序应删除功能。 驱动程序通常不会删除已由其他驱动程序设置的功能，但如果它在特定的配置中具有有关设备功能的特殊信息，则它可能会执行此操作。 请参阅[即插即用](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)，了解有关推迟 IRP 处理的信息，直到较低的驱动程序完成。

枚举设备及其驱动程序时，其功能不应更改。 如果删除并重新枚举设备，则设备的功能可能会改变。

当处理**irp\_MN\_QUERY\_功能**IRP 时，设备的电源策略管理器的驱动程序应该设置*IoCompletion*例程并复制设备电源功能，如 S 到 D 电源状态按照 IRP 的方式备份设备堆栈。 为了确定子设备的电源功能，父总线驱动程序会创建另一个查询功能 IRP，并将 IRP 发送到其父驱动程序。 有关详细信息，请参阅[报表设备电源功能](https://docs.microsoft.com/windows-hardware/drivers/kernel/reporting-device-power-capabilities)。

如果驱动程序处理此 IRP，它应检查**设备\_功能** **版本**值。 如果该值不是驱动程序所支持的版本，则该驱动程序应该会使 IRP 失败。 如果支持该版本，则驱动程序应检查 "**大小**" 字段。 驱动程序只应设置在作为输入接收的功能结构边界内的字段。

处理此 IRP 的驱动程序可以 **\_功能**字段设置某些设备，但不得设置 "**大小**" 和 "**版本**" 字段。 这些字段仅由发送 IRP 的组件设置。

请参阅[即插即用](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)，了解用于处理[即插即用次要 irp](plug-and-play-minor-irps.md)的一般规则。

**正在发送此 IRP**

当总线驱动程序处理**irp\_MN\_查询**其某个子设备的\_功能请求时，它会将该 irp 发送到父设备堆栈。 另外，驱动程序可能会发送此 IRP，以获取其某个设备的设备功能。 堆栈中的单个驱动程序只包含设备的功能信息的一部分;将 IRP 发送到设备堆栈使其能够收集完整的图片，包括任何筛选器驱动程序的修改等。

有关发送 Irp 的信息，请参阅[处理 irp](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-irps) 。 以下步骤专门适用于此 IRP：

-   从页面缓冲池分配[**设备\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)结构，并通过调用[**RtlZeroMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlzeromemory)将其初始化为零。 将**大小**初始化为**sizeof**（**设备\_功能**），将**版本**初始化为1，将**Address**和**UINumber**初始化为-1。

-   在 IRP 的下一个 i/o 堆栈位置设置值：将**MajorFunction**设置为[**irp\_MJ\_PNP**](irp-mj-pnp.md)，将**MINORFUNCTION**设置为**irp\_MN\_查询\_功能**，并设置**DeviceCapabilities**指向分配的设备的指针 **\_功能**结构。

-   将**IoStatus**初始化\_不\_支持的状态。

-   如果不再需要 IRP 和**设备\_功能**结构，请将其解除分配。

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


[**设备\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)

 

 




