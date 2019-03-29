---
title: IRP_MN_DEVICE_USAGE_NOTIFICATION
description: 系统组件发送此 IRP 询问设备是否可以支持的特殊文件的设备驱动程序。
ms.date: 08/12/2017
ms.assetid: d8287ba2-ac0a-4407-b587-a5aa5b3617a2
keywords:
- IRP_MN_DEVICE_USAGE_NOTIFICATION 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: 2ce83261421bbddb47b3653a6ddff1e0707256c8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562940"
---
# <a name="irpmndeviceusagenotification"></a>IRP\_MN\_DEVICE\_USAGE\_NOTIFICATION


系统组件发送此 IRP 询问设备是否可以支持的设备驱动程序*特殊文件*。 特殊文件包括分页文件、 转储文件和休眠文件。 如果这些设备的所有驱动程序成功 IRP，系统会创建特殊的文件。 系统还会发送通知的驱动程序的特殊文件已从设备中删除此 IRP。

功能的驱动程序必须处理此 IRP，如果分页文件、 转储文件或休眠文件可以包含其设备。 如果将筛选功能驱动程序处理 IRP，筛选器驱动程序必须处理此 IRP。 总线驱动程序必须处理此 IRP 为其适配器或控制器 （总线 FDO） 和为其子设备 (子 PDOs)。

<a name="major-code"></a>主代码
----------

[**IRP\_MJ\_PNP**](irp-mj-pnp.md) When Sent
---------

它是创建或删除页面文件、 转储文件或休眠文件时，系统会发送此 IRP。 如果设备具有超出了传统的父-子关系的电源管理关系，该驱动程序可以发送此 IRP 传播到另一个设备堆栈的设备使用情况信息。 有关详细信息，请参阅的说明**PowerRelations**中请求[ **IRP\_MN\_查询\_设备\_关系**](irp-mn-query-device-relations.md).

系统组件和驱动程序在 IRQL 被动发送此 IRP\_级别在任意线程上下文中。

## <a name="input-parameters"></a>输入参数


**Parameters.UsageNotification.InPath**的成员[ **IO\_堆栈\_位置**](https://msdn.microsoft.com/library/windows/hardware/ff550659)结构是一个布尔值。 当此参数是 **，则返回 TRUE**、 系统创建分页，故障转储或设备上的休眠文件。 当**InPath**是**FALSE**，已从设备中删除此类文件。

**Parameters.UsageNotification.Type**是一个枚举，该值指示的文件的类型。 此参数具有以下值之一：**DeviceUsageTypePaging**， **DeviceUsageTypeDumpFile**，或**DeviceUsageTypeHibernation**。

## <a name="output-parameters"></a>输出参数


无

## <a name="io-status-block"></a>I/O 状态块


驱动程序集**Irp-&gt;IoStatus.Status**于状态\_成功或相应的错误状态。

驱动程序不会修改**Irp-&gt;IoStatus.Information**字段; 它仍然保持为零，由发送 IRP 的组件设置。

<a name="operation"></a>操作
---------

驱动程序处理此 IRP IRP 的向下设备堆栈和 IRP 的方式备份在堆栈上。

驱动程序的响应如下所示的过程与此 IRP 到：

-   如果**Parameters.UsageNotification.InPath**是**TRUE**，确定设备是否支持特殊文件。

    驱动程序应测试的特定**Parameters.UsageNotification.Type**(s) 的驱动程序支持。 可能在将来添加其他通知类型。

    请参阅下面描述支持每种通知类型所需的操作的进一步信息。

    如果**Parameters.UsageNotification.InPath**是**TRUE**和驱动程序不能支持设备上的特殊文件，该驱动程序必须完成 IRP 失败状态。

-   如果设备支持特殊的文件：

    1.  采取适当措施，以反映设备现在包含，或不再包含的特殊文件。

        驱动程序通常递增或递减一个计数器。 例如，如果**Parameters.UsageNotification.Type**是**DeviceUsageTypePaging**并**Parameters.UsageNotification.InPath**是**TRUE**，递增的设备上的分页文件数的计数。 某些驱动程序调度例程必须检查计数器。

        不应禁用包含的特殊文件的设备。 驱动程序可以调用[ **IoInvalidateDeviceState**](https://msdn.microsoft.com/library/windows/hardware/ff549361)，请求的即插即用的管理器进行重新查询设备的即插即用设备状态信息。 为生成的响应[ **IRP\_MN\_查询\_PNP\_设备\_状态**](irp-mn-query-pnp-device-state.md) IRP，驱动程序应设置 PNP\_设备\_不\_DISABLEABLE 标志。

        如果**InPath**是**FALSE**，驱动程序设置执行\_POWER\_PAGABLE 位在其设备的设备对象。

    2.  将传播到任何需要的信息的相关设备的设备使用情况信息。

        作为其处理的一部分**IRP\_MN\_设备\_用法\_通知**IRP，驱动程序可能需要将信息传递给一个或多个其他设备堆栈。 此类驱动程序创建一个新**IRP\_MN\_设备\_用法\_通知**IRP （或 Irp） 并将其发送到相应的设备堆栈 （或堆栈）。 该驱动程序必须等待完成的任何设备使用情况通知 IRP(s) 驱动程序完成处理收到的设备使用情况 IRP 之前发送。

        如何识别相关的设备是特定于设备和驱动程序。 通常情况下，驱动程序将 IRP 发送到其他驱动程序会将该文件的 I/O 请求发送。 当总线驱动程序处理此请求的子设备时，它必须向设备堆栈中的设备的父发送使用情况通知 IRP。

        例如，当 ftdisk 运行 5 个磁盘条带集时，它可传播寻呼通知发送到每个五个磁盘，由于每个这些设备可以需要处理分页文件操作。

    3.  在函数或筛选器驱动程序，将[ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)例程。

    4.  在函数或筛选器驱动程序，将**Irp-&gt;IoStatus.Status**于状态\_成功后，设置下一步堆栈的位置，并将 IRP 传递到下一个较低的驱动程序与[ **IoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff548336)。 无法完成 IRP。

        针对子级 PDO 处理 IRP 到总线驱动程序： 设置**Irp-&gt;IoStatus.Status**并完成 IRP ([**IoCompleteRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548343))。

    5.  期间 IRP 完成处理：

        如果*IoCompletion*例程检测到较低的驱动程序失败 IRP，该函数或筛选器驱动程序必须撤消以响应 IRP 它执行任何操作并传播错误。 如果该函数或筛选器驱动程序传播到任何其他设备堆栈的使用情况信息，该驱动程序必须将另一个用法 IRP 发送到这些堆栈，以通知他们失败。

        如果状态是状态\_成功并**InPath**是**TRUE**，清除执行\_POWER\_PAGABLE 位。

请参阅[插](https://msdn.microsoft.com/library/windows/hardware/ff547125)处理的常规规则[即插即用次要 Irp](plug-and-play-minor-irps.md)。

**支持分页、 故障转储，以及在设备上的休眠文件**

当任何驱动程序的特殊文件计数不为零时，驱动程序必须支持在其设备 （或子代设备） 上的特殊文件存在。

有关**DeviceUsageTypePaging**其设备驱动程序上创建的文件必须执行以下操作：

-   在内存中锁定代码及其[ *DispatchRead*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)， [ *DispatchWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)， [ *DispatchDeviceControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)，并[ *DispatchPower* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程。

-   清除 DO\_电源\_PAGABLE 位在其设备的设备对象中 （在设备堆栈中向上 IRP 的方式）。

-   失败**IRP\_MN\_查询\_停止\_设备**并**IRP\_MN\_查询\_删除\_设备**设备的请求。

有关**DeviceUsageTypeDumpFile**文件在其设备上，驱动程序必须执行以下操作：

-   在内存中锁定代码及其*DispatchRead*， *DispatchWrite*， *DispatchDeviceControl*，以及*DispatchPower*例程。

-   不会在设备从 D0 状态。

    未注册为空闲检测设备 ([**PoRegisterDeviceForIdleDetection**](https://msdn.microsoft.com/library/windows/hardware/ff559721))。 如果已注册设备时，取消注册。 如果驱动程序执行其自身空闲检测设备时，挂起此类检测。

-   清除 DO\_电源\_PAGABLE 位在其设备的设备对象中 （在设备堆栈中向上 IRP 的方式）。

-   失败[ **IRP\_MN\_查询\_停止\_设备**](irp-mn-query-stop-device.md)并[ **IRP\_MN\_查询\_删除\_设备**](irp-mn-query-remove-device.md)设备的请求。

有关**DeviceUsageTypeHibernation**文件在其设备上，驱动程序必须执行以下操作：

-   在内存中锁定代码及其*DispatchRead*， *DispatchWrite*， *DispatchDeviceControl*，以及*DispatchPower*例程。

-   请确保设备在驱动程序收到 S4 系统电源 IRP，该值指示系统即将进入休眠状态时处于 D0 状态。

-   执行不关闭响应 D3 集功率设备 IRP，属于 S4 休眠状态操作。 请参阅[系统电源操作](https://msdn.microsoft.com/library/windows/hardware/ff564553)有关详细信息。

    收到此类 D3 集 power IRP，执行将设备放在关闭设备电源和通知电源管理器除外 D3 状态所需的所有任务 ([**PoSetPowerState**](https://msdn.microsoft.com/library/windows/hardware/ff559765))。 已写入休眠文件之前，设备必须保留电源。

-   清除 DO\_电源\_PAGABLE 位在其设备的设备对象中 （在设备堆栈中向上 IRP 的方式）。

-   失败[ **IRP\_MN\_查询\_停止\_设备**](irp-mn-query-stop-device.md)并[ **IRP\_MN\_查询\_删除\_设备**](irp-mn-query-remove-device.md)设备的请求。

请参阅[电源管理](https://msdn.microsoft.com/library/windows/hardware/ff547131)有关设备的电源状态的详细信息，支持 Irp，并在驱动程序中支持电源管理。

**发送此 IRP**

驱动程序可以发送**IRP\_MN\_设备\_用法\_信息**IRP，但仅以设备使用情况将信息传播到另一个设备堆栈。 驱动程序永远不会是初始的设备使用情况信息源。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Wdm.h 中 （包括 wdm.h 中、 Ntddk.h 或 Ntifs.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[*DispatchDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)

[*DispatchPower*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)

[*DispatchRead*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)

[*DispatchWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)

[**IoAdjustPagingPathCount**](https://msdn.microsoft.com/library/windows/hardware/ff548209)

[**IoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff548336)

[**IoCompleteRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548343)

[**IO\_堆栈\_位置**](https://msdn.microsoft.com/library/windows/hardware/ff550659)

[**IRP\_MJ\_PNP**](irp-mj-pnp.md)

[**IRP\_MN\_查询\_设备\_关系**](irp-mn-query-device-relations.md)

[**IRP\_MN\_QUERY\_PNP\_DEVICE\_STATE**](irp-mn-query-pnp-device-state.md)

[**IRP\_MN\_查询\_删除\_设备**](irp-mn-query-remove-device.md)

[**IRP\_MN\_查询\_停止\_设备**](irp-mn-query-stop-device.md)

[**PoRegisterDeviceForIdleDetection**](https://msdn.microsoft.com/library/windows/hardware/ff559721)

[**PoSetPowerState**](https://msdn.microsoft.com/library/windows/hardware/ff559765)

 

 




