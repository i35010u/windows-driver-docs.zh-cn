---
title: IRP_MN_QUERY_DEVICE_RELATIONS
description: PnP 管理器发送此请求，以确定设备之间的某些关系。
ms.date: 08/12/2017
ms.assetid: 32437c5a-ad92-433c-8255-83775751a44d
keywords:
- IRP_MN_QUERY_DEVICE_RELATIONS 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: 55884e623edc843a066488d474c8140effdeae4c
ms.sourcegitcommit: 7681ac46c42782602bd3449d61f7ed4870ef3ba7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/07/2020
ms.locfileid: "82922586"
---
# <a name="irp_mn_query_device_relations"></a>IRP\_MN\_查询\_设备\_关系


PnP 管理器发送此请求，以确定设备之间的某些关系。 以下类型的驱动程序处理此请求：

-   总线驱动程序必须处理其适配器或控制器（bus FDO）的**BusRelations**请求。 筛选器驱动程序可能会处理**BusRelations**请求。

-   总线驱动程序必须处理其子设备（子 PDOs）的**TargetDeviceRelation**请求。

-   函数和筛选器驱动程序可能会处理**RemovalRelations**和**PowerRelations**请求。

-   总线驱动程序可以处理其子设备（子 PDOs）的**EjectionRelations**请求。

## <a name="value"></a>值

0x07

<a name="major-code"></a>主要代码
----------

[**IRP\_MJ\_PNP**](irp-mj-pnp.md)

<a name="when-sent"></a>发送时间
---------

PnP 管理器发送此 IRP，收集与指定设备有关系的设备的相关信息。

当设备处于活动状态时，PnP 管理器会查询设备的**BusRelations** （子设备），而在其他情况下，该设备处于活动状态，例如当驱动程序调用[**IoInvalidateDeviceRelations**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinvalidatedevicerelations)例程来指示子设备已到达或 departed。

PnP 管理器会在删除设备驱动程序之前查询设备的**RemovalRelations** 。 PnP 管理器会在**RemovalRelations**和**EjectionRelations**弹出设备之前对其进行查询。

当驱动程序或用户模式应用程序注册设备上的**EventCategoryTargetDeviceChange**的 pnp 通知时，PnP 管理器会查询设备的**TargetDeviceRelation** 。 PnP 管理器查询与特定文件对象关联的设备。 **IRP\_MN\_查询\_设备\_关系**是唯一具有有效 file object 参数的 PnP IRP。 驱动程序可以为**TargetDeviceRelation**查询设备堆栈。 驱动程序在发送其**TargetDeviceRelation**查询时无需提供文件对象。

当设备的驱动程序调用**IoInvalidateDeviceRelations**时，PnP 管理器会查询设备的**PowerRelations** ，以指示此设备具有隐式电源管理关系的设备集已发生更改。 从 Windows 7 开始支持**PowerRelations**请求。

对于**BusRelations**、 **RemovalRelations**、 **EjectionRelations**和**PowerRelations**请求，PnP 管理器会在系统线程的上下文中发送**IRP\_MN\_查询\_设备\_关系**，以 IRQL = 被动\_级别。

对于**TargetDeviceRelation**请求，PnP 管理器会在任意线程上下文中以\_IRQL = 被动级别发送此 IRP。

## <a name="input-parameters"></a>输入参数


[**IO\_堆栈\_位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)结构的**QueryDeviceRelations**成员指定正在查询的关系的类型。 可能的值包括**BusRelations**、 **EjectionRelations**、 **RemovalRelations**、 **TargetDeviceRelation**和**PowerRelations**。

仅当**QueryDeviceRelations**为**TargetDeviceRelation**时，当前**IO\_\_堆栈位置**结构的**FileObject**成员才指向有效的文件对象。

## <a name="output-parameters"></a>输出参数


在 i/o 状态块中返回。

## <a name="io-status-block"></a>I/o 状态块


驱动程序将**Irp-&gt;IOSTATUS**设置为状态\_"成功" 或设置为 "失败" 状态\_，\_如 "资源不足"。

成功时，驱动程序将**&gt;IoStatus**设置为指向请求的关系信息\_的 PDEVICE 关系指针。 **设备\_关系**结构定义如下：

```cpp
typedef struct _DEVICE_RELATIONS {
  ULONG  Count;
  PDEVICE_OBJECT  Objects[1];  // variable length
} DEVICE_RELATIONS, *PDEVICE_RELATIONS;
```

<a name="operation"></a>操作
---------

如果驱动程序在响应此**IRP\_\_MN 查询\_设备\_关系**时返回关系，则驱动程序将从分页内存中分配一个**设备\_关系**结构，该结构包含计数和适当数量的设备对象指针。 当不再需要该结构时，PnP 管理器会将其释放。 如果驱动程序替换了另一驱动程序分配的**设备\_关系**结构，则驱动程序必须释放以前的结构。

驱动程序必须引用它在此 IRP 中报告的任何设备的 PDO （[**ObReferenceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obfreferenceobject)）。 PnP 管理器会在适当时删除引用。

函数或筛选器驱动程序应准备好在设备的[*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)例程完成后，为设备处理此 IRP。 枚举设备后，应准备好总线驱动程序来处理**BusRelations**的查询。

有关处理[即插即用次要 irp](plug-and-play-minor-irps.md)的一般规则，请参阅[即插即用](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)。

以下小节介绍了用于处理各种查询的特定操作。

**BusRelations 请求**

如果 PnP 管理器查询适配器或控制器的总线关系（子设备），则总线驱动程序必须返回指向总线上物理上存在的任何设备的 PDOs 的指针列表。 总线驱动程序报告所有设备，无论它们是否已启动。 总线驱动程序可能需要为总线设备接通电源，以确定哪些子项存在。

**警告**   ：无法将设备对象传递到采用 PDO 作为参数的任何例程，直到 PnP 管理器为该对象创建设备节点（*devnode*）。 （如果驱动程序已通过设备对象，则系统将使用[**Bug 检查检查错误码 0xca\_： PNP 检测到\_\_错误**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xca--pnp-detected-fatal-error)。）PnP 管理器将创建 devnode，以响应**IRP\_MN\_查询\_设备\_关系**请求。 驱动程序可以安全地假定在收到[**IRP\_MN\_\_查询资源\_要求**](irp-mn-query-resource-requirements.md)请求时已创建了 PDO 的 devnode。

 

响应此 IRP 的总线驱动程序是总线适配器或控制器的函数驱动程序，而不是适配器或控制器连接到的总线的父总线驱动程序。 非总线设备的函数驱动程序不处理此查询。 此类驱动程序只需将 IRP 传递到下一个较低版本的驱动程序。 （请参见下图。）筛选器驱动程序通常不处理此查询。

在 Windows Vista 和更高版本的操作系统上，建议驱动程序始终**挂起\_IRP\_MN\_QUERY\_设备关系**IRP 并在以后完成其处理。 此顺序使系统可以异步处理总线关系查询。 （在 Windows Vista 之前的操作系统上，驱动程序可以安全\_地从其调度例程返回 "挂起" 状态，但 PnP 管理器不会与任何其他操作重叠总线关系查询。）

下图显示了驱动程序如何处理总线关系的查询。

![阐释处理总线关系查询的驱动程序的关系图](images/qdrstaks.png)

在图所示的示例中，PnP 管理器将**IRP\_MN\_查询\_设备\_关系** **BusRelations**到 USB 集线器设备的驱动程序。 PnP 管理器正在请求集线器设备子节点的列表。

1.  与所有 PnP Irp 一样，PnP 管理器将 IRP 发送到设备在设备堆栈中的顶层驱动程序。

2.  可选筛选器驱动程序可能是堆栈中的顶层驱动程序。 筛选器驱动程序通常不处理此 IRP;它将 IRP 向下传递到堆栈。 筛选器驱动程序可能会处理此 IRP，例如，当驱动程序在总线上公开不可枚举的设备时。

3.  USB 集线器总线驱动程序处理 IRP。

    USB 集线器总线驱动程序：

    -   为尚未包含任何子设备的任何子设备创建一个 PDO。

    -   将不在总线上的任何设备的 PDO 标记为非活动状态。 总线驱动程序不会删除此类 PDOs。有关何时删除 PDOs 的详细信息，请参阅[删除设备](https://docs.microsoft.com/windows-hardware/drivers/kernel/removing-a-device)。

    -   报告总线上存在的任何子设备。

        对于每个子设备，总线驱动程序都引用 PDO，并在设备\_关系结构中放置一个指向 pdo 的指针。

        在此示例中有两个 PDOs：一个用于操纵杆设备，另一个用于键盘设备。

        总线驱动程序应检查是否有另一个驱动程序已\_为此 IRP 创建了设备关系结构。 如果是这样，则总线驱动程序必须将添加到现有的信息中。

        如果总线上不存在子设备，驱动程序会在设备\_关系结构中将计数设置为零，并返回 success。

    -   在 i/o 状态块中设置相应的值，并将 IRP 传递到下一个较低的驱动程序。 适配器或控制器的总线驱动程序未完成 IRP。

4.  可选的低筛选器（如果有）通常不处理此 IRP。 此类筛选器驱动程序将 IRP 向下传递到堆栈。 如果较低的筛选器驱动程序处理此 IRP，它可以将 PDO 添加到子设备列表，但不能删除其他驱动程序创建的任何 PDOs。

5.  父总线驱动程序不处理此 IRP，除非它是设备堆栈中唯一的驱动程序（设备处于 raw 模式）。 与所有 PnP Irp 一样，父总线驱动程序完成 IRP with [**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)。

    如果设备堆栈中有一个或多个总线筛选器驱动程序，此类驱动程序可能会将 IRP 处理到总线驱动程序上，并/或通过 IRP 的方式备份设备堆栈（如果存在[*IoCompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)例程）。 根据 PnP IRP 规则，此类驱动程序可以将 PDOs 添加到其沿堆栈下的方式，并/或修改 IRP 上的关系列表（在*IoCompletion*例程中）。

**EjectionRelations 请求**

驱动程序将指针返回到在弹出指定设备时可能会从系统中实际删除的任何设备的 PDOs。 不报告设备子的 PDOs;PnP 管理器始终请求在其父设备之前删除子设备。

PnP 管理器会将[**irp\_MN\_弹出**](irp-mn-eject.md)IRP 发送到要弹出的设备。 此类设备的驱动程序还会接收 "删除 IRP"。 设备的弹出关系接收[**irp\_\_MN REMOVE\_device**](irp-mn-remove-device.md) irp （而不是**irp\_MN\_EJECT** IRP）。

只有父总线驱动程序可以响应其某个子设备的**EjectionRelations**查询。 函数和筛选器驱动程序必须将其传递到设备堆栈中的下一个较低的驱动程序。 如果总线驱动程序接收到此 IRP 作为适配器或控制器的函数驱动程序，则总线驱动程序将执行函数驱动程序的任务，并且必须将 IRP 传递到下一个较低版本的驱动程序。

**PowerRelations 请求**

从 Windows 7 开始， **PowerRelations**查询使驱动程序能够指定支持 PnP 枚举的父总线与总线上的枚举子设备之间的传统关系的电源管理关系。 例如，如果总线驱动程序无法枚举总线上的子设备，或者设备是多个总线的子，则**PowerRelations**查询可以描述子设备与总线的电源关系。

当设备的驱动程序调用[**IoInvalidateDeviceRelations**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinvalidatedevicerelations)例程并指定**PowerRelations**的*类型*参数值时，PnP 管理器会为设备发出**PowerRelations**查询。

对于此查询，目标设备的驱动程序（即，查询的目标设备）提供了一个**设备\_关系**结构，该结构包含指向任何其他设备的 PDOs 的指针，这些设备必须在打开目标设备之前由电源管理器打开。 相反，只有在关闭目标设备后，才能关闭这些其他设备。 Power manager 使用查询中的信息来保证按正确的顺序打开和关闭这些设备。

此顺序保证仅适用于全局系统睡眠状态转换，包括与 S1、S2、S3 （*睡眠*）、S4 （*休眠*）和 S5 （*关机*）系统电源状态之间的转换。 **PowerRelations**顺序保证不适用于 Dx 设备电源状态转换，而系统仍处于 S0 （*正在运行*）系统状态，但[定向运行时电源管理（DFx）](https://docs.microsoft.com/windows-hardware/drivers/kernel/introduction-to-the-directed-power-management-framework)转换除外。

如果目标设备位于特殊文件（如页面文件、休眠文件或故障转储文件）的设备路径上，则目标设备的驱动程序在处理[**irp\_MN\_设备\_使用\_通知**](irp-mn-device-usage-notification.md)IRP （其中**InPath**为**TRUE**）时，必须执行额外的步骤。 此驱动程序必须确保为**PowerRelations**查询提供其 PDOs 的设备也可以支持在特定文件的设备路径中。 若要确认此支持，目标设备的驱动程序必须首先将**\_irp MN\_设备\_使用情况\_通知**IRP 发送到其中每个设备，并且此 IRP 必须指定与目标设备相同的**UsageNotification。** 仅当接收此 IRP 的所有设备完成 IRP 并显示成功状态代码时，目标设备的驱动程序才能成功完成其**irp\_MN\_设备\_使用\_通知**IRP。 否则，此驱动程序必须使用故障状态代码完成此 IRP。

当此同一驱动程序处理**InPath**为**FALSE**的**\_IRP MN\_设备\_使用情况\_通知**irp 时，驱动程序必须将**irp\_MN\_设备\_使用\_情况通知**irp 发送到相同的依赖设备集，这是因为**InPath**为**TRUE**。 但是，当**InPath**为**FALSE**时，驱动程序不应在失败状态代码的情况下完成此 IRP。

响应**PowerRelations**查询的驱动程序应在为**PowerRelations**查询提供 PDOs 的所有设备上注册目标设备更改通知。 若要注册这些通知，驱动程序可以调用[**IoRegisterPlugPlayNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterplugplaynotification)例程，并将*EventCategory*参数值指定为**EventCategoryTargetDeviceChange**。

**RemovalRelations 请求**

驱动程序将指针返回到在删除指定设备的驱动程序时必须删除其驱动程序的任何设备的 PDOs。 不报告设备子的 PDOs;PnP 管理器已请求删除子设备，然后才能删除设备。

删除删除关系的顺序是不确定的。

设备堆栈中的任何驱动程序都可以处理此类型的关系查询。 函数或筛选器驱动程序在将 IRP 传递到下一个较低版本的驱动程序之前对其进行处理。 总线驱动程序处理 IRP，然后完成。

**TargetDeviceRelation 请求**

使用**TargetDeviceRelation**查询，pnp 管理器可以在用于控制硬件的 PnP 设备堆栈中查询 PDO 的非 PnP 设备堆栈。

通常，驱动程序将**irp\_MN\_查询\_设备\_关系**IRP 向下转发到其堆栈，直到 irp 达到特定设备堆栈的底部。 非 PnP 堆栈底部的驱动程序，然后将 IRP 转发或重新颁发给相关的 PnP 堆栈。 例如，PnP 管理器可能会将**TargetDeviceRelation**查询发送到文件系统堆栈顶部的设备对象，这是一个非 PnP 堆栈。 文件系统堆栈中的每个设备对象会将查询传递给其下的设备对象，直到该查询到达堆栈底部的设备对象。 堆栈中的最小设备对象会将**TargetDeviceRelation**查询转发或重新发出到 PnP 存储卷堆栈顶部的设备对象，然后将查询向下传递到存储卷堆栈底部的 PDO。

下面的列表总结了可以安全获取指向 PnP 设备堆栈底部的 PDO 的指针的情况：

-   PnP 中的设备对象

    当调用设备的[*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)例程时，PnP 设备堆栈中的设备对象将了解堆栈的 PDO。 如果使用指针与传入[**IRP\_MN\_\_**](irp-mn-remove-device.md)通过使用[删除锁定例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)来删除设备消息，则驱动程序可以安全地缓存指向 PDO 的指针。

-   非 PnP 堆栈中的设备对象，而不是堆栈底部的设备对象

    对于非 PnP 堆栈底部的设备对象，驱动程序可以发送**TargetDeviceRelation**查询，以获取指向对应的 PnP 设备堆栈底部的 PDO 的指针。

-   设备的文件对象

    给定设备的文件对象，驱动程序可以调用[**IoGetRelatedDeviceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetrelateddeviceobject)来获取设备对象，然后按照前面的列表项中的说明进行操作。

-   设备对象的句柄

    给定设备对象的句柄，驱动程序可以调用[**ObReferenceObjectByHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbyhandle)来获取设备的文件对象，然后按照前面的列表项中的说明进行操作。

父总线驱动程序必须处理子设备的**TargetDeviceRelation**关系查询。 总线驱动程序通过[**ObReferenceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obfreferenceobject)引用子设备的 pdo，并返回指向**设备\_关系**结构中的 PDO 的指针。 此关系类型的结构中只有一个 PDO 指针。 当驱动程序或应用程序在设备上注销通知时，PnP 管理器将删除对 PDO 的引用。

只有父总线驱动程序才会响应**TargetDeviceRelation**查询。 函数和筛选器驱动程序必须将其传递到设备堆栈中的下一个较低的驱动程序。 如果总线驱动程序接收到此 IRP 作为适配器或控制器的函数驱动程序，则总线驱动程序将执行函数驱动程序的任务，并且必须将 IRP 传递到下一个较低版本的驱动程序。

如果驱动程序不在基于 PDO 的堆栈中，则驱动程序会将新的目标设备关系查询 IRP 发送到与驱动程序在其上执行 i/o 的文件句柄关联的设备对象。

**正在发送此 IRP**

驱动程序不得发送**IRP\_MN\_查询\_设备\_关系**来请求**BusRelations**。 对于**RemovalRelations**或**EjectionRelations**，驱动程序不限于发送此 IRP，但驱动程序不太可能会这样做。

驱动程序可以在设备堆栈中查询**TargetDeviceRelation**。 有关发送 Irp 的信息，请参阅[处理 irp](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-irps) 。 以下步骤专门适用于此 IRP：

-   在 IRP 的下一个 i/o 堆栈位置设置值：将**MajorFunction**设置为[**irp\_\_MJ PNP**](irp-mj-pnp.md)，将 MinorFunction 设置为**irp\_MN\_查询\_设备\_关系**，将**MinorFunction**设置为**TargetDeviceRelation**，并将**IRP-&gt;FileObject**设置为有效的文件对象。 **Parameters.QueryDeviceRelations.Type**

-   将**IoStatus**初始化为不\_受\_支持的状态。

如果驱动程序发送此 IRP 以获取 PDO 来响应该驱动程序收到的**TargetDeviceRelation**的**\_IRP\_MN\_\_查询设备关系**，则驱动程序将报告 PDO 并在 IRP 完成时释放返回的关系结构。 如果驱动程序出于其他原因启动了此 IRP，则当 IRP 完成时，驱动程序将释放关系结构，并且在不再需要该 PDO 时取消对它的引用。

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


[*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)

[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)

[**IoGetRelatedDeviceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetrelateddeviceobject)

[**IoInvalidateDeviceRelations**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinvalidatedevicerelations)

[**IoRegisterPlugPlayNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterplugplaynotification)

[**IRP\_MJ\_PNP**](irp-mj-pnp.md)

[**IRP\_MN\_设备\_使用\_通知**](irp-mn-device-usage-notification.md)

[**IRP\_MN\_弹出**](irp-mn-eject.md)

[**IRP\_MN\_查询\_资源\_需求**](irp-mn-query-resource-requirements.md)

[**IRP\_MN\_删除\_设备**](irp-mn-remove-device.md)

[**IO\_堆栈\_位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)

[**ObReferenceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obfreferenceobject)

[**ObReferenceObjectByHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbyhandle)

 

 




