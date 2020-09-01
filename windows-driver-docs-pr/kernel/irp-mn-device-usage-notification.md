---
title: IRP_MN_DEVICE_USAGE_NOTIFICATION
description: 系统组件发送此 IRP 来询问设备的驱动程序是否可以支持特殊文件。
ms.date: 08/12/2017
ms.assetid: d8287ba2-ac0a-4407-b587-a5aa5b3617a2
keywords:
- IRP_MN_DEVICE_USAGE_NOTIFICATION 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: 5c89fec6a946dd0f740e15b28c37721c8e3d4cbd
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89185189"
---
# <a name="irp_mn_device_usage_notification"></a>IRP \_ MN \_ 设备 \_ 使用 \_ 通知


系统组件发送此 IRP 来询问设备的驱动程序是否可以支持 *特殊文件*。 特殊文件包括页面文件、转储文件和休眠文件。 如果设备的所有驱动程序都成功完成 IRP，系统会创建该特殊文件。 系统还会发送此 IRP，通知驱动程序已从设备中删除特殊文件。

如果功能驱动程序的设备可包含页面文件、转储文件或休眠文件，则它必须处理此 IRP。 如果筛选器驱动程序正在筛选的函数驱动程序处理 IRP，则筛选器驱动程序必须对其进行处理。 总线驱动程序必须为其适配器或控制器 (总线 FDO) 及其子设备处理此 IRP (子 PDOs) 。

## <a name="value"></a>值

0x16

<a name="major-code"></a>主要代码
----------

[**IRP \_ MJ \_ PNP**](irp-mj-pnp.md)

<a name="when-sent"></a>发送时间
---------

系统在创建或删除页面文件、转储文件或休眠文件时发送此 IRP。 如果设备的电源管理关系超出了常规父子关系，则驱动程序可以发送此 IRP 将设备使用情况信息传播到另一个设备堆栈。 有关详细信息，请参阅[**IRP \_ MN \_ 查询 \_ 设备 \_ 关系**](irp-mn-query-device-relations.md)中的**PowerRelations**请求说明。

系统组件和驱动程序 \_ 在任意线程上下文中以 IRQL 被动级别发送此 IRP。

## <a name="input-parameters"></a>输入参数


[**IO \_ 堆栈 \_ 位置**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)结构的**UsageNotification. INPATH**成员是一个布尔值。 如果此参数为 **TRUE**，则系统将在设备上创建分页、崩溃转储或休眠文件。 当 **InPath** 为 **FALSE**时，将从设备中删除此类文件。

**UsageNotification** 是指示文件类型的枚举。 此参数具有以下值之一： **DeviceUsageTypePaging**、 **DeviceUsageTypeDumpFile**或 **DeviceUsageTypeHibernation**。

## <a name="output-parameters"></a>输出参数


无

## <a name="io-status-block"></a>I/o 状态块


驱动程序将 **Irp- &gt; IoStatus** 状态设置为 " \_ 成功" 或相应的 "错误" 状态。

驱动程序不会修改 ** &gt; IoStatus** 字段; 它保持为零，由发送 Irp 的组件设置。

<a name="operation"></a>操作
---------

驱动程序按照 IRP 在设备堆栈上的方式来处理此 IRP，并按 IRP 上的方式备份堆栈。

驱动程序使用如下所示的过程来响应此 IRP：

-   如果 **InPath** 为 **TRUE**，则确定设备是否支持特殊文件。

    驱动程序应测试特定 **参数。 UsageNotification** (s) 驱动程序可以支持。 将来可能会添加其他通知类型。

    有关详细信息，请参阅下面的详细信息，介绍支持每种通知类型所需的操作。

    如果 **InPath** 为 **TRUE** ，并且驱动程序无法支持设备上的特殊文件，则驱动程序必须以失败状态完成 IRP。

-   如果设备支持特殊文件：

    1.  采取相应的措施，以反映设备现在包含或不再包含特殊文件。

        驱动程序通常会递增或递减计数器。 例如，如果 **UsageNotification** 是 **DeviceUsageTypePaging** ， **UsageNotification. InPath** 为 **TRUE**，则递增设备上页面文件数量的计数。 某些驱动程序调度例程必须检查计数器 (s) 。

        不应禁用包含特殊文件的设备。 驱动程序可以调用 [**IoInvalidateDeviceState**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinvalidatedevicestate)，请求 PnP 管理器重新查询设备的 PnP 设备状态信息。 为了响应生成的 [**IRP \_ MN \_ 查询 \_ PNP \_ 设备 \_ 状态**](irp-mn-query-pnp-device-state.md) IRP，驱动程序应设置 PNP \_ device \_ NOT \_ DISABLEABLE 标志。

        如果 **InPath** 为 **FALSE**，则驱动程序会 \_ \_ 在设备的设备对象中设置 DO POWER PAGABLE 位。

    2.  将设备使用情况信息传播到任何需要该信息的相关设备。

        作为 **IRP \_ MN \_ 设备 \_ 使用 \_ 通知** irp 处理的一部分，驱动程序可能需要将信息传递给一个或多个其他设备堆栈。 此类驱动程序将创建新的 **IRP \_ MN \_ 设备 \_ 使用情况 \_ 通知** IRP (或 irp) 并将它们发送到相应的设备堆栈 (或堆栈) 。 驱动程序必须等待设备使用情况-通知 IRP (的完成，然后该驱动程序在处理收到的设备使用 IRP 之前发送) 。

        如何识别相关设备特定于设备和驱动程序。 通常，驱动程序会将 IRP 发送到它向其发送文件的 i/o 请求的其他驱动程序。 当总线驱动程序为子设备处理此请求时，它必须将使用情况通知 IRP 发送到设备的父设备的设备堆栈。

        例如，当 ftdisk 运行的是5个磁盘的条带集时，它会将分页通知传播到这五个磁盘中的每个磁盘，因为每个设备都需要处理分页文件操作。

    3.  在函数或筛选器驱动程序中，设置 [*IoCompletion*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine) 例程。

    4.  在函数或筛选器驱动程序中，将 " ** &gt; IoStatus** " 设置为 " \_ 成功" 状态，设置下一个堆栈位置，并将 Irp 传递到下一个较低的驱动程序和 [**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)。 不要完成 IRP。

        在处理子 PDO 的 IRP 的总线驱动程序中：设置 **irp- &gt; IoStatus** 并完成 IRP ([**IoCompleteRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)) 。

    5.  完成 IRP 处理期间：

        如果 *IoCompletion* 例程检测到较低版本的驱动程序失败了 irp，则函数或筛选器驱动程序必须撤消它为对 irp 做出响应并传播错误而执行的任何操作。 如果函数或筛选器驱动程序将使用情况信息传播到任何其他设备堆栈，则驱动程序必须将另一个使用 IRP 发送到这些堆栈，以通知它们发生了故障。

        如果状态为 \_ "成功" 并且 **InPath** 为 **TRUE**，请清除 "DO \_ POWER PAGABLE" \_ 。

请参阅 [即插即用](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play) ，了解用于处理 [即插即用次要 irp](plug-and-play-minor-irps.md)的一般规则。

**支持设备上的分页、故障转储和休眠文件**

当驱动程序的任何特殊文件计数为非零值时，驱动程序必须支持在其设备 (或子代设备) 上存在特殊文件 () 。

对于在其设备上创建的 **DeviceUsageTypePaging** 文件，驱动程序必须执行以下操作：

-   为 [*DispatchRead*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)、 [*DispatchWrite*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)、 [*DispatchDeviceControl*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)和 [*DispatchPower*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程锁定内存中的代码。

-   清除设备堆栈) 上的 "在设备上 (的设备" 对象中的 "DO \_ POWER \_ PAGABLE" 位。

-   失败 **IRP \_ MN \_ 查询 \_ 停止 \_ 设备** 和 **IRP \_ MN \_ 查询 \_ 删除 \_ ** 设备请求。

对于其设备上的 **DeviceUsageTypeDumpFile** 文件，驱动程序必须执行以下操作：

-   为 *DispatchRead*、 *DispatchWrite*、 *DispatchDeviceControl*和 *DispatchPower* 例程锁定内存中的代码。

-   请勿使设备退出 D0 状态。

    请勿将设备注册到空闲检测 ([**PoRegisterDeviceForIdleDetection**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-poregisterdeviceforidledetection)) 。 如果设备已注册，则取消注册。 如果驱动程序对设备执行其自己的空闲检测，请挂起此类检测。

-   清除设备堆栈) 上的 "在设备上 (的设备" 对象中的 "DO \_ POWER \_ PAGABLE" 位。

-   失败 [**IRP \_ MN \_ 查询 \_ 停止 \_ 设备**](irp-mn-query-stop-device.md) 和 [**IRP \_ MN \_ 查询 \_ 删除 \_ **](irp-mn-query-remove-device.md) 设备请求。

对于其设备上的 **DeviceUsageTypeHibernation** 文件，驱动程序必须执行以下操作：

-   为 *DispatchRead*、 *DispatchWrite*、 *DispatchDeviceControl*和 *DispatchPower* 例程锁定内存中的代码。

-   当驱动程序收到一个 S4 系统电源 IRP，指示系统即将进入休眠状态时，请确保设备处于 D0 状态。

-   请勿关闭设备以响应作为 S4 睡眠操作一部分的 D3 集电源 IRP。 有关详细信息，请参阅 [系统电源操作](./system-power-actions.md) 。

    收到此类 D3 集电源 IRP 后，执行将设备置于 D3 状态所需的所有任务，但关闭设备并通知电源管理器 ([**PoSetPowerState**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-posetpowerstate)) 。 设备必须保持电源，才能写入休眠文件。

-   清除设备堆栈) 上的 "在设备上 (的设备" 对象中的 "DO \_ POWER \_ PAGABLE" 位。

-   失败 [**IRP \_ MN \_ 查询 \_ 停止 \_ 设备**](irp-mn-query-stop-device.md) 和 [**IRP \_ MN \_ 查询 \_ 删除 \_ **](irp-mn-query-remove-device.md) 设备请求。

有关设备电源状态、电源 Irp 和驱动程序中的电源管理的详细信息，请参阅 [电源管理](./introduction-to-power-management.md) 。

**正在发送此 IRP**

驱动程序可以发送 **irp \_ MN \_ 设备 \_ 使用情况 \_ 信息** irp，但只将设备使用情况信息传播到另一个设备堆栈。 驱动程序绝不会成为设备使用情况信息的初始来源。

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
<td>Wdm.h（包括 Wdm.h、Ntddk.h 或 Ntifs.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[*DispatchDeviceControl*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

[*DispatchPower*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

[*DispatchRead*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

[*DispatchWrite*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

[**IoAdjustPagingPathCount**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioadjustpagingpathcount)

[**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)

[**IoCompleteRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)

[**IO \_ 堆栈 \_ 位置**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)

[**IRP \_ MJ \_ PNP**](irp-mj-pnp.md)

[**IRP \_ MN \_ 查询 \_ 设备 \_ 关系**](irp-mn-query-device-relations.md)

[**IRP \_ MN \_ 查询 \_ PNP \_ 设备 \_ 状态**](irp-mn-query-pnp-device-state.md)

[**IRP \_ MN \_ 查询 \_ 删除 \_ 设备**](irp-mn-query-remove-device.md)

[**IRP \_ MN \_ 查询 \_ 停止 \_ 设备**](irp-mn-query-stop-device.md)

[**PoRegisterDeviceForIdleDetection**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-poregisterdeviceforidledetection)

[**PoSetPowerState**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-posetpowerstate)

 

